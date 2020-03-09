---
title: 'FordLabs React-Native: an approach to dev machine setup'
author: Matt Trueblood
tags: 'React-Native, X-code, Android Studio'

---

<h1 id="one-way-to-react-native-at-fordlabs">One way to React-Native at FordLabs</h1>
<p>Building native apps for 2 platforms hurts so React-Native might be a better solution. You do have to install twice the tooling to get yourself up and running, and the Ford proxies/IT policies don’t exactly make this a breeze. I found one way to get it done which is below but please <strong>seek the council of dharr419</strong> as he is probably the most experienced at this.</p>
<p>Software that must be installed to get your app running and with local simulation:</p>
<ol>
<li>Node/NPM</li>
<li>Watchman</li>
<li>React-Native CLI</li>
<li>Android Studio</li>
<li>Xcode</li>
</ol>
<h2 id="install-nodenpm">Install Node/NPM</h2>
<p>Let’s use Homebrew to get Node and watchman at the same time:</p>
<pre><code>brew install node watchman
</code></pre>
<p>You probably already have them installed so it will simply tell you what version you are running, but otherwise it will install them.</p>
<h2 id="install-react-native-cli">Install React-Native CLI</h2>
<p>We’ll use npm to pull this in globally:</p>
<pre><code>npm install -g react-native-cli
</code></pre>
<p>‘react-native-cli’ is an older method that uses Android Studio and Xcode for local simulation. There is another path you can take to run your app on a physical device by connecting to Wifi called <a href="https://docs.expo.io/versions/latest/get-started/installation/">Expo</a>.</p>
<p>Getting the Wifi connection working for Expo was more hassle than it was worth for me, but setting up expo itself is definitely faster than the Android Studio/Xcode route so you may want to look into this.</p>
<h2 id="install-android-studio">Install Android Studio</h2>
<p>Click to <a href="https://developer.android.com/studio">download the installer</a>. Open Android Studio. Choose custom install. Check the boxes for</p>
<ul>
<li>Android SDK</li>
<li>Android SDK Platform</li>
<li>Performance(Intel@HAXM) - this speeds up the simulator.</li>
<li>Android Virtual Device</li>
</ul>
<p>Begin downloads.</p>
<p>Once it’s installed open it up and click on Configure on the splash page. Under System settings select Android SDK, and then select the Show Package Details checkbox. Then open the Android version(s) that you are targeting and tick the following boxes:</p>
<ul>
<li>Google APIs</li>
<li>Intel x86 Atom_64 System Image</li>
<li>Google APIs Intel x86 Atom_64 System Image</li>
</ul>
<h2 id="install-xcode-no-appstore">Install Xcode (no AppStore)</h2>
<p>It would be nice if we could just install from AppStore but at the time I’m writing this it’s not possible. If that is still the case then we can download a .xip file and install it ourselves.</p>
<ol>
<li>Go to the <a href="https://developer.apple.com/develop/">Apple Developer page</a>,   click on downloads and sign in</li>
<li>At the bottom of the page click See More Downloads</li>
<li>Search for “Xcode”</li>
<li>Find the version you want and click on the plus button</li>
<li>Click download on the zip file</li>
</ol>
<p>This is a large file so after it downloads you just have to click on the Xcode[VERSION].xip file to install the program. Then move it to the Applications folder.</p>
<p>Run this command to see where Xcode <em>thinks</em> it is located:</p>
<pre><code> xcode-select  --print-path
</code></pre>
<p>If this doesn’t show the path as being /Applications/Xcode.app you should run this command to fix the issue:</p>
<pre><code>sudo xcode-select  --switch  /Applications/Xcode.app
</code></pre>
<h2 id="other-setup-stuff">Other setup stuff</h2>
<p>We need to append a bit to our bash profile so add the following to the end of your profile:</p>
<pre><code>alias android-studio="open -a /Applications/Android\ Studio.app/"
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
</code></pre>
<p>Once you have done this run the command:</p>
<pre><code>source $HOME/.bash_profile
</code></pre>
<p>To confirm that this worked you can just echo out the path to look for the correct location for the SDK.</p>
<h2 id="lets-test-it">Let’s test it</h2>
<p>In a terminal cd to workspace or wherever you want to build a test project and run the following command:</p>
<pre><code>npx react-native init &lt;APP_NAME&gt;
</code></pre>
<p>This will of course run a long-ish set of installation commands, but everything should work properly. If it doesn’t just google the error messages (you’ll probably just need to brew install some dependency).</p>
<p>Change directory into the folder for your test application and run npm install. Once that is done you can run the following commands to bring your test application up in a simulator.</p>
<h4 id="simulate-in-ios-nice-and-easy">Simulate in iOs: <em>(Nice and easy)</em></h4>
<pre><code>react-native run-ios
</code></pre>
<p>Allow the build to run, and look to the new iterm tab that should open up running Metro Bundler to see when the application should load into the Xcode simulator. As long as you are seeing a basic home screen everything should be working fine.</p>
<p>To enable hot-reloading press <code>CMD + d</code></p>
<h4 id="simulate-in-android-not-as-easy">Simulate in Android: <em>(Not as easy)</em></h4>
<p>From the root directory of your test app cd into the /android directory and run the command <code>android-studio .</code> which will open this project in Android Studio.</p>
<p>Find the AVD manager in the top right and click into it. Find a device or devices that you want to simulate with and download images for them in whatever version of Android you are targeting. Click next and then finish the dialog. The Virtual Device Manager will open up and you can use the actions to the right of any device in your list to start the device. Once you have an AVD running you can go back to the project root for the app and run the following:</p>
<pre><code>react-native run-android
</code></pre>
<p>Allow the build to run, and look to the new iterm tab that should open up running Metro Bundler to see when the application should load into the AVD. A couple of times I only got a black screen until I ran the following command:</p>
<p>To enable hot-reloading <code>CMD + m</code></p>
<h4 id="you-should-be-set-to-start-working-on-your-app-now">You should be set to start working on your “App” now!</h4>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

