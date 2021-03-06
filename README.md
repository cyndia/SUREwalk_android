<p align="center">
<img src="https://raw.github.com/pandanomic/SUREwalk_android/master/surewalk/src/main/res/drawable/surewalk_logo.png" alt="SUREwalk Logo" height="150" width="400"/>
</p>

[CHANGELOG](https://github.com/pandanomic/SUREwalk_android/blob/master/CHANGELOG.md)

### Members of the Android team include the following:
* [Guy Hawkins](https://github.com/GHawk1ns)
* [Chris Roberts](https://github.com/NASAgeek)
* [Henri Sweers](http://pandanomic.github.io)
* [Sam Thompson](https://github.com/st028)

Please note: commit history was not retained when transferring this repository to protect api keys.

### About
In the summer of 2013, a member of UT Student Government approached the Computer Science majors' Facebook group asking if anyone would be interested in helping them develop mobile apps for SUREwalk. SUREwalk is student-run, volunteer service where students can call at late hours of the night to have two volunteers come out and walk with them to wherever they need to go. SUREwalk wanted to improve their accessibility to students (before you just had to call them). We were more than happy to help with this cause.

Along with the Android side, other students also developed an iOS app and a website built with Rails, with all three platforms sharing a unified back end via Parse. If they opt to release that source code, we will post links here. 

We wanted to share this for the benefit of anyone else interested in developing an app for this purpose, or just developing an app itself.

### Basic Structure
* There is a main Dashboard Fragment that we use for the home screen, and displayed with a Twitter fragment (at their request) under a ViewPager
* The meat of the app is in the Request Activity. This is where we handled a paged request flow (we considered using WizardPager, but opted to roll our own instead). The steps of the flow are as follow:
  - Information: Name, EID, Phone, and E-Mail
  - Location: This is their start location, found either with the GPS or by entering an address to [Google's Geocoding API](https://developers.google.com/maps/documentation/geocoding/)
  - Destination: This is their destination, selected on a map displaying SUREwalk's boundaries
  - Review: This is the last step, allowing them to review their information and add any comments before submission.
* Throughout the Request flow, a ParseObject that mirrors one set up in our Parse database is constructed and fleshed out. Upon submission, this object is then saved to the Parse database, which is then polled by the Rails server to check for new requests.
* After SUREwalk receives the request and assigns it, a push notification is sent back using Parse+GCM to alert the user than the volunteers are on their way.

### Other stuff
If you want to build this on your own, you'll need to edit/create two files. One called `private_strings.xml` currently just holds dummy information, you'll need to populate it accordingly. The other is `com_crashlytics_export_strings.xml`, which is currently untracked (per Crashlytics' recommendations). This file is autogenerated if you set up crashlytics with your IDE. If you don't want to use it, simply comment out the Crashlytics startup code in the `onCreate()` method of MainActivity and `build.gradle`.

(All our private information is in an untracked private.md file)

### License
        The MIT License (MIT)

        Copyright (c) 2014 SUREwalk

        Permission is hereby granted, free of charge, to any person obtaining a copy
        of this software and associated documentation files (the "Software"), to deal
        in the Software without restriction, including without limitation the rights
        to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
        copies of the Software, and to permit persons to whom the Software is
        furnished to do so, subject to the following conditions:

        The above copyright notice and this permission notice shall be included in all
        copies or substantial portions of the Software.

        THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
        IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
        FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
        AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
        LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
        OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
        SOFTWARE.
