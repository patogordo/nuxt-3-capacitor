<script lang="ts" setup>
import { PushNotifications } from "@capacitor/push-notifications";
import type { PushNotificationSchema } from "@capacitor/push-notifications";
import { FCM } from "@capacitor-community/fcm";

const remoteToken = ref("");
const notifications = ref<PushNotificationSchema[]>([]);

onMounted(() => {
  PushNotifications.addListener("registration", (data) => {
    console.log(data);
  });
  PushNotifications.addListener(
    "pushNotificationReceived",
    (notification: PushNotificationSchema) => {
      console.log("notification " + JSON.stringify(notification));
      notifications.value.push(notification);
    }
  );
  PushNotifications.requestPermissions().then((response) =>
    PushNotifications.register().then(() => alert(`registered for push`))
  );
});

// move to fcm demo
const subscribeTo = () => {
  PushNotifications.register()
    .then((_) => {
      FCM.subscribeTo({ topic: "super-awesome-topic" })
        .then((r) => alert(`subscribed to topic ${"super-awesome-topic"}`))
        .catch((err) => console.log(err));
    })
    .catch((err) => alert(JSON.stringify(err)));
};

const unsubscribeFrom = () => {
  FCM.unsubscribeFrom({ topic: "super-awesome-topic" })
    .then((r) => alert(`unsubscribed from topic ${"super-awesome-topic"}`))
    .catch((err) => console.log(err));

  FCM.deleteInstance();
};

const getToken = () => {
  FCM.getToken()
    .then((result) => {
      remoteToken.value = result.token;
    })
    .catch((err) => console.log(err));
};
</script>
<template>
  <div>
    <h1>Hello World d</h1>

    <h2>Token: {{ remoteToken }}</h2>

    <button @click="getToken">Get token</button>
    <button @click="subscribeTo">Sub</button>

    <br />

    <h2>Notifications:</h2>

    {{ JSON.stringify(notifications) }}
  </div>
</template>

