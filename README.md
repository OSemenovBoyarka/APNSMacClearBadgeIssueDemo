# APNSMacClearBadgeIssueDemo

This demo project is slightly modified version of original Apple [PushyMac](https://developer.apple.com/library/mac/samplecode/PushyMac/Introduction/Intro.html) sample.

## Description

The issue is - dock icon badge seems to have some cache, and that cache is not synced, while you update badge value programmatically, and by APNS, while app is not running.
So, if you send push notification with `"badge":1`, clear that badge in app, close app, and send another push with same `"badge":1` payload - dock icon will not change badge value.
However if you send push with `"badge":2` - icon badge will change.

## Reproduce instructions
1. Build and launch included sample
2. Send push notification with following payload `{"aps":{"alert":"New message","badge":1,"sound":"default"}}`
3. See app's dock icon badge is set to **"1"** (it's fine)
4. Press "Ok" on Alert
5. See app's dock icon badgeis set to **"0"** (it's fine)
6. Option+Click on Dock icon - Options - Check "Keep in dock"
7. Close app
8. Send push notification with following payload `{"aps":{"alert":"Another new message","badge":1,"sound":"default"}}`

**Expeted result:** dock icon badge should be set to **"1"**
**Actual result:** dock icon badge is not changed

9. To ensure badge sets up, while app is closed - send another push notification with payload `{"aps":{"alert":"Two new messages","badge":2,"sound":"default"}}`
**Expeted result:** dock icon badge should be set to **"2"**
**Actual result:** dock icon badge is set to **"2"** (all works fine)
