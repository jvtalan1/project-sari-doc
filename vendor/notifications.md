# Creating push notification

Creating a push notification that will be visible on all platforms must follow the format:

Sample push notification:

```
{
  title: "Push notification title",
  body: "Your push notification content will go here",
  data: {
    title: "Another title or same as above",
    body: "More content or same as above"
  },
  channel_id: "AndroidChannelId",
  subtitle: "Subtitle for iOS"
}
```

The `data` field may or may not be included, however, if you choose to exclude data from the notification, it will be displayed as is on the notification bar but it will not be displayed in your inbox. Also, if you opt to include `data` in your notification, make sure to include `title` and `body` for it to be properly displayed on the mobile phone. Data can be used to give more information about your notification that a notification display may not have.
