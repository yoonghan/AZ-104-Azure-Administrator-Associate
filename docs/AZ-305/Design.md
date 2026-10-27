# Design

Designing a music-sharing application in Azure.
* Notify users when new **music** is uploaded to Azure.
* Users must be able to decide they want to access new music.

Use `Azure Queue Storage`, as this is a this is a Pull design. Giving user to **decide** when they want to access new music. `Azure Grid` seems plausible but it's a Push sending message but user will get notification and cannot be "decided".

