>> MARTIN HELLSPONG: So I got some water and I accidentally got sparkling water, which isn't a good idea before I talk.
But I was so nervous, it's not sparkling anymore.
So I think it's good.
Oh.
I have my password.
It's just star, star, star, star.
Really, I forgot this one.
Oh.
it works.
Okay.
So my name is Martin Hellspong.
I work at factor 10.
I'm a software initial there and we are based in Sweden and it's awesome to be here at Rustment really?
It's there it's not there?
I also didn't start the time recording, right?
So let's do that.
(Pause).



I'm still not there?
Yes.
So it's awesome to be at RustFest and I'm here to talk about QuickCheck, which is a test method that is under appreciated, I think.
And the reason is that it helps you find bugs that traditional testing often don't find.
And there have been case studies, showing that you find more bugs with less effort per bug, using QuickCheck.
And that's a nice promise fur.
And traditional testing it works by very fine expected behavior and perhaps you poke around some of the expected edge cases.
I haven't changed my slide.
So I'm where I'm -- both slides.
It's just that I have a long intro and setting you up for all kinds of failure.
Any way, and now, you lost me.
The reason for this is that this isn't optimal because you write your own tests, and you won't surprise yourself.
But the randomness will actually surprise you and your code.
So that's why QuickCheck uses randomness to generate hundreds of thousands or like, any number of test cases you want, according to a specification, and randomness gives, the power to give varied test cases.
As an example, there was a bug file against Google's level DB.
They hadn't -- Google hadn't found it with traditional.
But that's because it needed a sequence of 17API calls to trigger the consistency part.
And quick check found this by someone writing a test for quick check that, explored and looked for inconsistencies and see randomness.
We can all agree, no one writes a standard unit test, at least that long.
So my ambition with this talk is to get you excited about using this if your problems and I'm not going to be very Rust-specific so most of what I'm saying is applicable to quick check in randomized testing in general.
You should be able to take something out of your projects.
Okay.
QuickCheck.
There's variance able from most almosts, now, but it originated in the research community about 1999.
Worked from [indiscernible] and John Hughes, and John use Hughes is author of functioning paper.



You need to make a testable statement about your code.
For example, say that they're written in absolutely amazing summation function.
And can you make a statement about that, say something like, my summation function makes a list of integers and returns positive integer always.
And the traditional test method, it's like you're an intern.
You and your co-worker, sounds like it's working.
Because I used it in one test and it worked.
But QuickCheck is more like your know-it-all co-worker.
But he won't take your word for T.
we have run hundreds of test cases to see if your statement actually works: So it looks like the significant of your statement a lot of test cases, try to find a counter example.
If it does, or if it doesn't, and if it does -- it has a test case used to prove you wrong.
And this is how continued look in code.
This summation function.
Just takes list of integer and it's so awesome I didn't even include the limitation.
Then you have your statement, which is something like a function that's posted.
Takes the list of numbers and give us you the Boolean.



Succeeds, returns true all the time.
In this case, probably what will happen is it will say something lib was posted, it failed, when given the example, the example is the list of the number minus 1.
Negative number, obviously, it wouldn't be positive.
So that's QuickCheck helping you find discrepancies between your code and standpoint.
Perhaps in this characters summation function should have onsite integers or your assumption how it works, you should find a different statement.



How does it know how to generate test cases?
Well, for primitives these funks are built in.
Counter example, QuickCheck does something called shrinking to minimize the test case.
You can also provide a custom type.
But that's seldom necessary.
The possibility is there.
QuickCheck now introduces randomness into your builds.
And people will say stuff like, we don't want unstable tests.
You must know who broke the bill.
What change did they do to make it fail.
What if it poses QA and fails the release without any changes.
I mean, that's valid criticisms.
Some processes doesn't handal randomness and on the level of individual developer, I mean, you do a big fix ands in not fixed.
Or is it just because of failure case wasn't generated.
Or you ad a test failure.
Does a failure case happen to be [indiscernible].
However, in practices, often, much more stable than you would think when you heard randomness.
It's not like it flips flops.
It works because you generate hundreds of test cases.
If you have some case that's only generated once in every 200 test cases, 100, perhaps it flops and flips between.
But otherwise, it's mostly in my experience, they always at the same time they are programmatic.
But we must remember, the correct decisions now we introduce untable tests.
An unstable test is something with the same input gets two different ruts.
You don't know Y.
but the unlikely case, it happens and then you get the counter example.
That's when given this, it always return this is failure.
So you need to take good care for example, and you can produce a unit test.



You can also tweak a generator, if you have generator for your type.
You can tweak that to generate cases more often.
On the process level, we could look at fixing the seat to the random number generator.
However, that trades test coverage for stability, which is not perhaps a good trade-off.
Depends on if you want to find box or you want your build to always work.
You can always give up.
You don't run a grid check test.
Perhaps you need traditional test and you could do [indiscernible] running, to see if you could flush out some bugs.



There's a tradeoff you need to make.
So now, we can look at how I use grid check.
So in my project, it's kind of a micro control.
I really like how the previous talks have geared into this.
It's very much helpful to have a couple of concepts explained.
It's kind of controlled projects.
Do I it on my experimental time.
So I get paid by but the company doesn't.
But think going that, it wasn't that funny to, not that exciting to do.
I want to do something more outrageous.
I probably need to make a simulated word, with a space shape, with a simulated micro controller, and then I knew what kind I wanted and see if you can guess which one it is.
This is the classic version of the Macintosh.
And commodore A minga 500.
This was the first so for those stack of reasons, I chose the processor, running all these few manslaughter.
The Motorola 68,000.
And also 40 years old, the computers.
Or the processor, rather.
So it's possible to emulate it.
Something like 18 megahertz.



So now in reality, we have a simulated micro controller problems.
8,000 CPU which is often called M68K.
I took an existing C library, running in the main emulators.
And I report that to RustFest and I decided to do this, rather recklessly, as project write up.
And it's called R68K.
And it's off of GitHub.
It isn't fully functional yet, but it's useful.
For me.
If you look at regulator what you need to test this.

It's only 58 instructions.
So possibly, can you just write 56 units.
However, this doesn't really work because it's annex plosion ever instructions, data sites, registers, and you can release for one single code and there's 64,000 value of up codes, and about 11,000 I think its has done transition, anyway, so I knew then, I needed quick check.
I couldn't possibly write enough tests.
So how diuse it?
I basically made a statement.
There's two CPU's.
They should behave Identically.
And by identically.
Giving random initial states.
Execute one instruction ethical.
And it's very fine state is shaping the content of registers and memory, as well as old memory access are correct size and alignment and what not.



Then I thought, QuickCheck, just go ahead and approve me on this.
And it did, repeatedly.
Remorsesly.
Lee and ultimately helpful.
I ended up with 1,600 QuickCheck tests.
One test is testing combination of register and covers all the possible cases.
Hundreds of trials each.
Running all the tests, is something like three hours, 45 minutes.
So single threaded so I can't run parallel.
I've used gnu parallel to run cargo in parallel, the tests.
It's one test per instance, I ended up doing 16PR's.
Elements like cycle counts.
How many cycles it took.
And I had a single complex statement about the identical behavior.
You don't need to have a perfect comparison.
This statement was much simply in the beginning, it was still very, very useful to get something and as soon as you take the statement and improve it.
It will improve this test.
Now to run a more thorough comparison.
I'm very happy to say, verified with QuickCheck.
I'm basically, 100% sure.
And if you for all the instructions.
I still have work to do with exceptions and stuff, still provides me a use value.
Let's look at the bigger picture.
Not talking about my project anymore.
I could talk about this for hours but you'll have to catch me tomorrow.
So we could here, take a look at a statement, what is the problem of the statement.
It's hard to, when you start using QuickCheck, it's hard to come up with different kind of staples.
You normally, write the unit test F.
input 42, I should get this back.
But saying for any number that hold, it's not that useful.
So now, I get to the fact part and fact part is just saying something about your code.
There's basically F I back up a little bit, there's three different things about statements.
Effectses, inverse functions, and there's compare WGS a known good one.
Facts will already -- we have already seen.
Summation function.
Inverse is something like encode, decode.
You encrypt something and then you then decrypt it.
It should return the same value.
If you compares pare something with a non-good, one thing you can use the verged of your code.
If you have an implication, and it had a very nice indication of something, it was slow, but it worked.
Then if you need to do a performance, you can have your QuickCheck round against your standard non-optimized case and compare it against the optimized case.
With kacheing.
-- cacheing.



The guy drove an idealistic model of the database, with capabilities and ran that together with level, and check that they matched all the time.
The model is much simpler.
It could be a memory carried.
You don't need to make all the guarantees.
You can also take existing code.
That's the third one.
And one of them is third party which I was using.
You can have the old verged of your code.
If you have version one that does something interesting and you want to do a reimplementation of that and you want it to be as good.
You can compare verged 1 and version 2.
So I have skipped one thing.
What happens if you have irrelevant cases, you want to discard those when you're testing.
There's also an example of an inverse assemble.
Thank you for mentioning those.
Now, have you to return a test result.
What you do S you have a function.
This assemble, San off code, which is basically, 16 bits.
If you disassemble T you should have a -- not all codes are valued.
If it is not valued, it'll return an error.
Don't bother doing this test now because it's not valued because I can't assemble but if it happens to be valued, I get some successly text.
Being be something like are like, [indiscernible] to 3, to 2 points.



In code we test if you assemble this text, do you get the same code.
You started with, and you create the test result from that.
And this means that test all the places where disassemble works.
Assemble should work.



I also want to mention, other place where is QuickCheck is used.
I think it was 107.
They all use QuickCheck.
Ether tools, test fact about function u functions.
And the wide range, talking about Rust at all, ERICSSON is using to find race conscience in the database.
In the 4B based stations.
They tested integration.
Buy stuff from supplies and put it in their cars.
They found box in there communication and also found inconsistencies in there of the source.



I have one last story.
Level DB1.
It was even more absurd than the one I said.
There's a talk about this.
Land of jam, 1013.
A guy called John Orfton.
Found the 7th instant sequence that failed.
Google, provide aid fix.
He ran the same QuickCheck test.
Now after a cowl of minutes, found a 33 step sequence that reduces the same of inconsistency, and I think you can agree this is almost impossible to write the unitests, that would catch something like that.
So the wake away is, you won't surprise yourself.
Randomness will.
Stop worrying and learn to love the it.
Thank you very much.
