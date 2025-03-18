![image](https://github.com/user-attachments/assets/e0ffc1c6-77a3-49e9-a94b-09659193a7a4)

Creator - [Sasha Huang](https://github.com/umbresp)

This was a very interesting and unusual task, offering great variety and complexity.

---

Searching through channels and users ("utflag{..." and messages from Sasha) in the discord chat did not bring anything useful, which was actually expected judging by the number of people who solved this task.

Further OSINT outside Discord would also not bring anything:
==Note: The initial scope for this challenge is just the Discord server itself, and not any persons or individuals. Unofficial content is not in scope.==

And also these 2 more messages from admin led to the idea that we should think in a different direction:
![image](https://github.com/user-attachments/assets/c4bc27ce-b62e-4c0a-8e18-959c103a234c)


So I decided to check for hidden channels. The first search on the web showed this:
![image](https://github.com/user-attachments/assets/e169828f-748e-4106-ad17-dfcea8908737)

[ShowHiddenChannels](https://github.com/JustOptimize/ShowHiddenChannels) - BetterDiscord plugin.

I decided to try this plugin and for that it was necessary to set up BetterDiscord.

After installing, in the discord settings you will see the following:
![Pasted image 20250319005606](https://github.com/user-attachments/assets/701bcd3f-4202-4869-91b5-ece0eb6085cb)

then go to the Plugins tab and open plugins folder:
![174233149236158769](https://github.com/user-attachments/assets/2ee1c8e6-ac7b-4a46-a6f4-febd1f3d56b0)

move [ShowHiddenChannels.plugin.js](https://github.com/JustOptimize/ShowHiddenChannels/releases/download/v0.5.8/ShowHiddenChannels.plugin.js) file there and restart discord.

Accept the installation of the dependency and enable them in Plugins tab:
![Pasted image 20250319010508](https://github.com/user-attachments/assets/439ad5b4-3326-4e27-b39d-682a5f4230ff)
![Pasted image 20250319011053](https://github.com/user-attachments/assets/e036057f-1903-4967-b89f-35fdb63a7f25)

Changes can be noticed immediately(you might need to restart discord once more):
![Pasted image 20250319010706](https://github.com/user-attachments/assets/3fd35686-ef1a-45ac-9a1c-ae1a5c6600c5)![Pasted image 20250319010906](https://github.com/user-attachments/assets/1beadfb3-0e53-403a-a32c-aecf64797fe1)

And finally an interesting finding! **admin-only** channel:
![image](https://github.com/user-attachments/assets/1de59e84-b122-4d78-a33e-c303743ac602)

Write down the password somewhere and open the link.
[https://docs.google.com/document/d/1cgFhoHKLEbbJlu1SX4gCfFI4CGEEoEisiFq1CW-TKUo/edit?tab=t.0]

---  
# UTCTF 2025 Operational Notes

First of all lets visit the link, It takes us to a [GitHub gists](https://gist.github.com/umbresp/5275f23f615c9bdcb21c463ac4b87c3c) page.

Click revisions and decode the base64.
![image](https://github.com/user-attachments/assets/5d5b9894-016c-4999-a9bc-de8e4603bf6c)
![image](https://github.com/user-attachments/assets/41612e50-4b70-4c87-9f86-fc86bbaf3ffa)
[https://mega.nz/file/HHgR1RRL]







