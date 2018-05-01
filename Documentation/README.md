# Compose

Hi Orien and friends. I wanted to quickly leave you with some of my thoughts on this project as it's important, in the interview process, for you to understand how I approach problems.

# Challenges
Orien and I have briefly discussed that I've typically worked in the 3D space; with virtual reality, no less. Most of my UI experience tends to be fairly simplistic so this was a great way to stretch my legs and see if I could translate any of my skills into some a little flatter. Spoiler: I think I did!

### Recording Notes
This, in my opinion, is the meat of the challenge. Registering user input and creating feedback for the user is what makes this experience fun. I quickly determined that, if I know what note I'm pressing, and where the playhead is in the physical space, I know where each note sprite needs to be rendered. I haven't used Sprites too often but it's worth mentioning that I had to wrestle with the camera for awhile to get the playhead and notes in view. Some mindful layering did the trick.

Furthermore, I thought it was important that my recording remained independent of the playback, so as notes are being played, I'm capturing the key (by index), the time it was played, and constructing a KeyModel to be stored in a recording list of items. This was particularly useful for both playback and the reverse filter. See those sections for a little more.

### Playback
First, it was important that I locked down the UI during playback, else we would end up with unwanted note recordings.

Second, during playback, the easy approach would be to use the playhead collider to play notes as I "hit" them on the staff. However clever, I didn't feel good about relying on sprites to relay that information. Instead, when the user hits Playback, we iterate through our recorded items and generate invokers to play the audio clips.

Third, this made the Reverse Filter easier to create.

### Reverse Filter
When the user toggles Reverse on, the user can either record right to left or playback right to left (backwards). The Reverse toggle immediately signals Recorder to flip our List and update the time signatures on each note (5 seconds - the original time signature) so that they play appropriately in reverse.

### Quantization
I wasn't able to solve the extra credit in a meaningful amount of time. I want to get this back to you soon but I'll likely continue working on it tomorrow. But my idea is that, when a note is played, for each time signature, I can measure the difference between the signature and each setting to find the "nearest" appropriate value. I've used a similar approach in a recipe management program translating precise metric values into less precise Custom tablespoons, cups, etc.

I'll send it along if I've made substantial progress. It's definitely a time thing, not a logic thing.

# Design

### Diagrams
I'm huge on drawing ideas out so please swing by the Diagrams folder to see what I white boarded. I translated it from my whiteboard to draw.io because, you know, that was way more practical.

### Composition
I find Unity development typically has more opportunities for composition than any other object oriented principle. This wasn't a large program but a basic example would be how Staff owns Playhead. The Playhead lives on the Staff, and its position is determined by Staff's size/orientation, so this made sense.

### Delegation and Encapsulation
I tried to be very mindful about who had their hands in what business. I think, if I had a little more time, I could have done some things cleaner, but in general everything occurs in the same space; I'm not passing too much up/down the stack unnecessarily. An easy example would be that the Speaker script is solely responsible for all things audio while Recorder has its own List of recorded KeyNotes.

### Classes
 - Xylophone Manager: As main() as its going to get. The jumping off point for user input.
 - Timer: Songs live and die in the five seconds allotted! Best to manage it in one place.
 - Speaker: All things audible.
 - Staff: Owns Playhead and the Recorder. Our notes live here; physically and logically.
 - UI: Self explanatory, but StaffData does live on Staff. I could have used Find Component but, because its not a MonoBehavior, I just left it here. I'm not sure if it's a typical practice for Unity developers but I try to only use MonoBehaviors when I actually need them. Data models don't need to live on objects in the space, you know? My roommate, who is also a Unity developer, gets triggered when I try to employ .NETy MVC practices.

### UI
I was attempting to be particularly mindful about target platforms. This, being a 2D app, is obviously not my typical desktop 3D experience. So I employed some of my Android Studio knowledge and tried to make sure the UI elements were anchored appropriately. I didn't test whether or not it worked in both landscape and portrait but I wanted to mention that I did adjust the anchors, in a way, that I felt might help it scale better.

# In Closing
I'm a very deliberate programmer. I really like to puzzle about a problem for a long while before I even sit down to code. If I rush into things I tend to end up missing an opportunity to optimize or write clean code. So I wanted to thank you in advance for your patience.

I hope you're interested enough in me to have a follow up conversation about how I can contribute to the e-learning space with you. I'm super excited about what you do and would love to participate; as a junior engineer, an internship if it's more appropriate, or beyond.

Thank you!

Brandon