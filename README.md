# vista-higher-learning-app

### From within the app directory

- Run `npm i`
- Run `ionic serve`
- Run `ionic capacitor add` to add a native iOS or Android project using Capacitor
- Run `ionic build` to rebuild changes to platforms
- Run `ionic cap sync` to sync changes to platforms
- Run `ionic cap run` to run project for various platforms

## Explaination of Work...

I used the Ionic CLI to generate a new blank project,
which gave me the basic starting point. Then I went to work
adding the bits needed to accomplish the requirements.

Most of the intersting parts of this application are located
in src > HomePage.vue.

I chose Ionic as my component library since it comes with
a grid, icons, buttons and much more. I leveraged the power of
ionic grid to lay out the UI components, ionic buttons and radio
buttons were used and custom styled where possible. The behaviors
are accomplished using standard local state variables and common JS
functions made accessible to the template.

I had a mild concern about the requirements - three buttons are mentioned
early in the requirements as being "Stop", "Record" and "Review your recording".
Then, later under "7. Add some behaviors:" the requirements call out a "Play" button.
It's bad practice to make assumptions, but in the interest of completing the assignment
I assumed that the play button refered to the Record button, however these conditions
could be applied to either the Record or Review buttons with minor logic change. In
the real world I would reach out to clarify this misunderstanding :)

Enjoy!
