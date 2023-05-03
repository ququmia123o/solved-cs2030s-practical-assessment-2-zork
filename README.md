Download Link: https://assignmentchef.com/product/solved-cs2030s-practical-assessment-2-zork
<br>
<h3></h3>

<h4>Problem Description</h4>

If you think that a computer game requires stunning graphics, or least, cute ones, to be captivating, then you haven’t played Zork. Created in the late 1970s, before sound cards or graphics cards were invented, Zork was a text-only adventure game famed for its storytelling and advanced text parser. In it, you play the role of an explorer plonked in front of a house, surrounded by a forest, with no hint of what your goal might be: whether to rescue an imprisoned princess, or to find hidden treasure.

You interact by typing commands, such as “GO NORTH”, or “HIT THE TROLL WITH THE ELVISH SWORD”, and the game responds with textual descriptions, such as “Phosphorescent mosses, fed by a trickle of water from some unseen source above, make the crystal grotto glow and sparkle with every color of the rainbow”. These words spark one’s imagination of mystery, fear, and adventure in ways that graphics and sound cannot.

Its commercial launch was a great success, spawning a trilogy (because otherwise the entire game could not fit into computer memory) that in total sold over 800,000 copies, and keeping it among the “Top 50 Games of All Time” even twenty years later. Zork foreshadowed, and influenced, the development of modern AI chatbots.

In this Practical Assessment (PA), you will create the basic game elements in Zork. While keeping it simple to fit the needs of a PA, there is great scope for future development into a much richer project for educational purpose (<i>read: talk to the Profs if you are interested</i>).

<h4>Task</h4>

In this task, you are only required to work with three things: a candle, a sword and a troll. These things are placed at possibly different rooms. The objective is to simulate and test different scenarios of game play. Take note of the following:

<ul>

 <li>all Java objects constructed are to be <i>immutable</i>;</li>

 <li>for simplicity, at no time will there be multiple things of the same type</li>

</ul>

This task is divided into several levels. You need to complete all levels. Read through all the levels to see how the different levels are related.

Remember to:

<ul>

 <li>write each class/interface/enum in a separate <tt>.java</tt> file</li>

 <li>always compile your program files first before using <tt>jshell</tt> to test your program</li>

 <li>declare object properties starting with <tt>private final</tt> or <tt>protected final</tt></li>

 <li>you may import any Java package; however do not use the wild card <tt>*</tt> in your import statements, else CodeCrunch will render your program uncompilable</li>

 <li>all tests use valid arguments; you need not check for validity of arguments; <tt>null</tt> will not be used for the tests</li>

</ul>




<h4>Level 1</h4>

Write a class <tt>Room</tt> to represent a room in the game. Things can be placed in a room. In this level, we shall place a <tt>Candle</tt> in the foyer. To simulate the passing of time, a method <tt>tick()</tt> in class <tt>Room</tt> is called.

With respect to the candle, every tick causes the candle to change state.The following are the state changes of the candle.

<ul>

 <li><tt>Candle flickers.</tt></li>

 <li><tt>Candle is getting shorter.</tt></li>

 <li><tt>Candle is about to burn out.</tt></li>

 <li><tt>Candle has burned out.</tt></li>

</ul>

Note that any <tt>tick</tt>s beyond the last state of the candle causes it to remain in it’s final state. Also, make sure that <tt>Room</tt> does not sub-class from any other class (apart from <tt>Object</tt> of course).




<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test1.jsh<b>jshell&gt; new Room("foyer");</b>$.. ==&gt; @foyer<b>jshell&gt; new Room("foyer").add(new Candle());</b>$.. ==&gt; @foyerCandle flickers.<b>jshell&gt; new Room("foyer").add(new Candle()).tick()</b>$.. ==&gt; @foyerCandle is getting shorter.<b>jshell&gt; new Room("foyer").add(new Candle()).tick().tick()</b>$.. ==&gt; @foyerCandle is about to burn out.<b>jshell&gt; new Room("foyer").add(new Candle()).tick().tick().tick()</b>$.. ==&gt; @foyerCandle has burned out.<b>jshell&gt; new Room("foyer").add(new Candle()).tick().tick().tick().tick()</b>$.. ==&gt; @foyerCandle has burned out.<b>jshell&gt; /exit</b></pre>

<h4>Level 2</h4>

Let’s now include two more things, <tt>Troll</tt> and <tt>Sword</tt>, into our room. Just like the candle, each of these things have their own states:

<ul>

 <li>For the Troll:

  <ul>

   <li><tt>Troll lurks in the shadows.</tt></li>

   <li><tt>Troll is getting hungry.</tt></li>

   <li><tt>Troll is VERY hungry.</tt></li>

   <li><tt>Troll is SUPER HUNGRY and is about to ATTACK!</tt></li>

   <li><tt>Troll attacks!</tt></li>

  </ul></li>

 <li>For the Sword:

  <ul>

   <li><tt>Sword is shimmering.</tt></li>

  </ul></li>

</ul>

Things are output in order of which they are added into the room. Also note that your program should be flexible enough for other things to be included in future.

<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test2.jsh<b>jshell&gt; Room foyer = new Room("foyer").add(new Candle()).add(new Troll())</b><b>jshell&gt; Stream.iterate(foyer, x -&gt; x.tick()).limit(6).forEach(System.out::println)</b>@foyerCandle flickers.Troll lurks in the shadows.@foyerCandle is getting shorter.Troll is getting hungry.@foyerCandle is about to burn out.Troll is VERY hungry.@foyerCandle has burned out.Troll is SUPER HUNGRY and is about to ATTACK!@foyerCandle has burned out.Troll attacks!@foyerCandle has burned out.Troll attacks!<b>jshell&gt; foyer = foyer.add(new Sword())</b><b>jshell&gt; Stream.iterate(foyer, x -&gt; x.tick()).limit(3).forEach(System.out::println)</b>@foyerCandle flickers.Troll lurks in the shadows.Sword is shimmering.@foyerCandle is getting shorter.Troll is getting hungry.Sword is shimmering.@foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering.<b>jshell&gt; foyer</b>foyer ==&gt; @foyerCandle flickers.Troll lurks in the shadows.Sword is shimmering.<b>jshell&gt; /exit</b></pre>

<h4>Level 3</h4>

Now, we are ready to interact with the objects. An interaction occurs by passing an action into an overloaded <tt>tick</tt> method that takes one argument. The action is in the form of a lambda that describes what actions to take on one or more things.

As an example, we can pass a dummy action <tt>x -&gt; x</tt> (the identity lambda) into <tt>tick</tt>. The test will take the following form:

<pre><b>jshell&gt; new Room("foyer").add(new Candle()).add(new Sword()).tick(x -&gt; x)</b>$.. ==&gt; @foyerCandle is getting shorter.Sword is shimmering.</pre>

As you can see, applying the dummy action above results in the same behaviour as

<pre><b>jshell&gt; new Room("foyer").add(new Candle()).add(new Sword()).tick()</b>$.. ==&gt; @foyerCandle is getting shorter.Sword is shimmering.</pre>

In addition, write the action <tt>takeSword</tt> into the file <tt>actions.jsh</tt>. Note that this will result in three different outputs (see sample run below) according to the state of things in the room. These output (prepended with <tt>"--&gt;"</tt>) must be specified within <tt>actions.jsh</tt> and not in the individual classes. You may choose any suitable types for the lambda.

<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order actions.jsh &lt; test3.jsh<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Sword()).tick(x -&gt; x)</b>$.. ==&gt; @foyerCandle is getting shorter.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Sword()).tick(x -&gt; x).tick(x -&gt; x)</b>$.. ==&gt; @foyerCandle is about to burn out.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Sword()).tick(takeSword)</b>--&gt; You have taken sword.$.. ==&gt; @foyerSword is shimmering.<b>jshell&gt; new Room("foyer").add(new Sword()).tick(takeSword).tick(takeSword)</b>--&gt; You have taken sword.--&gt; You already have sword.$.. ==&gt; @foyerSword is shimmering.<b>jshell&gt; new Room("foyer").tick(takeSword)</b>--&gt; There is no sword.$.. ==&gt; @foyer<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick()</b>$.. ==&gt; @foyerCandle is getting shorter.Troll is getting hungry.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick(x -&gt; x)</b>$.. ==&gt; @foyerCandle is getting shorter.Troll is getting hungry.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(x -&gt; x)</b>$.. ==&gt; @foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering.<b>jshell&gt; /exit</b></pre>

<h4>Level 4</h4>

Now add another action <tt>killTroll</tt> into <tt>actions.jsh</tt>. Look at the sample runs below for the behaviour of the action. Once again, the output (prepended with <tt>"--&gt;"</tt>) must be specified in <tt>actions.jsh</tt> and not in the respective class files. Also note that a killed troll will vanish from the room.

<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order actions.jsh &lt; test4.jsh<b>jshell&gt; new Room("foyer").add(new Sword()).tick(killTroll)</b>--&gt; There is no troll$.. ==&gt; @foyerSword is shimmering.<b>jshell&gt; new Room("foyer").add(new Sword()).add(new Troll()).tick(killTroll)</b>--&gt; You have no sword.$.. ==&gt; @foyerSword is shimmering.Troll is getting hungry.<b>jshell&gt; new Room("foyer").add(new Sword()).add(new Troll()).tick(takeSword).tick(killTroll)</b>--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @foyerSword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(takeSword)</b>--&gt; You have taken sword.$.. ==&gt; @foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(takeSword).tick(killTroll)</b>--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @foyerCandle has burned out.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(killTroll)</b>--&gt; You have no sword.$.. ==&gt; @foyerCandle is about to burn out.Troll is VERY hungry.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(killTroll).tick(takeSword)</b>--&gt; You have no sword.--&gt; You have taken sword.$.. ==&gt; @foyerCandle has burned out.Troll is SUPER HUNGRY and is about to ATTACK!Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).add(new Sword()).tick().tick(killTroll).tick(takeSword).tick(killTroll)</b>--&gt; You have no sword.--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @foyerCandle has burned out.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Candle()).add(new Troll()).tick(killTroll)</b>--&gt; You have no sword.$.. ==&gt; @foyerCandle is getting shorter.Troll is getting hungry.<b>jshell&gt; /exit</b></pre>

<h4>Level 5</h4>

We are now ready to venture into other rooms. Going into a room requires that a room be created first. This is done via the <tt>go</tt> method that takes in another lambda of the form <tt>x -&gt; new Room...</tt>. As an example, we can represent <i>deja vu</i> with the following test:

<pre><b>jshell&gt; new Room("dining").add(new Candle()).add(new Sword())</b>$.. ==&gt; @diningCandle flickers.Sword is shimmering.<b>jshell&gt; new Room("dining").add(new Candle()).add(new Sword()).go(x -&gt; new Room("mystery", x))</b>$.. ==&gt; @mysteryCandle flickers.Sword is shimmering.</pre>

Notice that this new mystery room that we just entered looks like the same room before! Not only that we can also bring an item that we picked into a new room.

<pre><b>jshell&gt; new Room("foyer").add(new Sword()).tick(takeSword).go(x -&gt; new Room("dining").add(new Candle()))</b>--&gt; You have taken sword.$.. ==&gt; @diningSword is shimmering.Candle flickers.</pre>

Note that things brought into a new room are listed first.

<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order actions.jsh &lt; test5.jsh<b>jshell&gt; new Room("dining").add(new Candle()).add(new Sword())</b>$.. ==&gt; @diningCandle flickers.Sword is shimmering.<b>jshell&gt; new Room("dining").add(new Candle()).add(new Sword()).go(x -&gt; new Room("mystery", x))</b>$.. ==&gt; @mysteryCandle flickers.Sword is shimmering.<b>jshell&gt; new Room("dining").add(new Candle()).tick().add(new Sword()).go(x -&gt; new Room("mystery", x))</b>$.. ==&gt; @mysteryCandle is getting shorter.Sword is shimmering.<b>jshell&gt; new Room("foyer").add(new Sword()).tick(takeSword).go(x -&gt; new Room("dining").add(new Candle()))</b>--&gt; You have taken sword.$.. ==&gt; @diningSword is shimmering.Candle flickers.<b>jshell&gt; Room r1 = new Room("foyer").add(new Candle())</b><b>jshell&gt; Room r2 = r1.go(x -&gt; new Room("library").add(new Sword()))</b><b>jshell&gt; Room r3 = r2.go(x -&gt; new Room("dining").add(new Troll()))</b><b>jshell&gt; r3.tick(killTroll)</b>--&gt; You have no sword.$.. ==&gt; @diningTroll is getting hungry.<b>jshell&gt; r2.tick(takeSword).go(x -&gt; new Room("dining").add(new Candle()).add(new Troll()))</b>--&gt; You have taken sword.$.. ==&gt; @diningSword is shimmering.Candle flickers.Troll lurks in the shadows.<b>jshell&gt; r2.tick(takeSword).go(x -&gt; new Room("dining").add(new Candle()).add(new Troll())).tick(killTroll)</b>--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @diningSword is shimmering.Candle is getting shorter.<b>jshell&gt; r1.go(x -&gt; new Room("library").</b><b>   ...&gt; add(new Sword()).</b><b>   ...&gt; tick(takeSword).</b><b>   ...&gt; go(y -&gt; new Room("dining").add(new Candle()).add(new Troll()))).tick(killTroll)</b>--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @diningSword is shimmering.Candle is getting shorter.<b>jshell&gt; /exit</b></pre>

<h4>Level 6</h4>

Finally, we would like to go back to the previous rooms. For simplicity, once we come back from a room, the room that we came back from vanishes, so we can’t go into it again. Note that when you return from room B to room A, things in room A are output first, followed by B (this is to be consistent with the output in the previous level dealing with <tt>go</tt>). That is to say, things in the room that is created earlier are always listed first. Also note that once we enter into a new room, and return from it, time in the original room ticks only once.

Lastly, add an action <tt>dropSword</tt> to drop the sword.

<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order actions.jsh &lt; test6.jsh<b>jshell&gt; Room r1 = new Room("foyer").add(new Candle())</b><b>jshell&gt; Room r2 = r1.go(x -&gt; new Room("dining").add(new Troll()))</b><b>jshell&gt; Room r3 = r2.go(x -&gt; new Room("library").add(new Sword()))</b><b>jshell&gt; r1</b>r1 ==&gt; @foyerCandle flickers.<b>jshell&gt; r2</b>r2 ==&gt; @diningTroll lurks in the shadows.<b>jshell&gt; r2.back()</b>$.. ==&gt; @foyerCandle is getting shorter.<b>jshell&gt; r2.tick().tick().tick()</b>$.. ==&gt; @diningTroll is SUPER HUNGRY and is about to ATTACK!<b>jshell&gt; r2.tick().tick().tick().back()</b>$.. ==&gt; @foyerCandle is getting shorter.<b>jshell&gt; r3</b>r3 ==&gt; @librarySword is shimmering.<b>jshell&gt; r3.back()</b>$.. ==&gt; @diningTroll is getting hungry.<b>jshell&gt; r3.back().back()</b>$.. ==&gt; @foyerCandle is getting shorter.<b>jshell&gt; r3.tick(takeSword).back().tick(killTroll).back()</b>--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @foyerCandle is getting shorter.Sword is shimmering.<b>jshell&gt; r3.tick(takeSword).back().tick(killTroll).tick(dropSword)</b>--&gt; You have taken sword.--&gt; Troll is killed.--&gt; You have dropped sword.$.. ==&gt; @diningSword is shimmering.<b>jshell&gt; r3.tick(takeSword).back().tick(killTroll).tick(dropSword).back()</b>--&gt; You have taken sword.--&gt; Troll is killed.--&gt; You have dropped sword.$.. ==&gt; @foyerCandle is getting shorter.<b>jshell&gt; r1.go(x -&gt; new Room("dining").add(new Troll())).</b><b>   ...&gt; tick().</b><b>   ...&gt; go(x -&gt; new Room("library").add(new Sword())).</b><b>   ...&gt; tick().</b><b>   ...&gt; tick(takeSword).</b><b>   ...&gt; back().</b><b>   ...&gt; tick().</b><b>   ...&gt; tick(killTroll)</b>--&gt; You have taken sword.--&gt; Troll is killed.$.. ==&gt; @diningSword is shimmering.<b>jshell&gt; /exit</b></pre>