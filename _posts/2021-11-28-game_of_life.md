---
title: 'An evening of coding: Game of Life'
---

When I had just started my career as software engineer I attended a course 'The Modern Developer' by [Sebastien Lambla](https://serialseb.com/about/). He used [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life) as an example problem.  I remember thinking it could be a fun thing to code, but never found the time.

And now, a little over 4 years later, I was stuck at home one evening and decided it is finally time to do it. I chose plain Ruby for this, as I only use Rails at work and usually work only on already set up projects. Building something from scratch seemed like a treat in itself.

Here is the result I made with [Curses gem](https://rubygems.org/gems/curses/versions/1.2.4). I have some sort of weird nostalgia for the old days of software engineering (that I did not get to experience) with all the cumbersome text user interfaces. 
<video width="640" muted autoplay controls >
    <source src="/assets/videos/game_of_life.mp4" type="video/mp4">
</video>
<br/>
Some interesting things I've noticed while working on this:

__How elegant Ruby is__

- My initial approach was to just print grids to console one by one. In order to make the dead cells stand out, I looked for ways to add color to the output. And came across [colorize gem](https://github.com/fazibear/colorize). You simply need to assign color to your string like 
```
DEAD = X.red
```
And that's it! The console output will be colored. I think that is extremely neat!

- I modeled my grid as two dimensional array. First I was iterating through rows and columns separately, but at some point I thought '_maybe I am missing some more Ruby-ish way to do it?_'. And I found a [stack overflow post](https://stackoverflow.com/questions/1296739/how-to-iterate-over-an-array-of-arrays) that showed this is indeed enough:
```
grid.each do |row, cell|
    cell.do_something
end
```
What I liked the most about this was a comment under the answer: _2 years with ruby. And it's still fascinating._

__How differently people feel about test fixtures__

- I was writing some tests with [RSpec](https://relishapp.com/rspec/) and at some point decided to add [FactoryBot gem](https://rubygems.org/gems/factory_bot/versions/4.8.2) for test fixtures. I really liked how the end result looked like and how little data needed to be changed for each test case and how easy it was to do that with the fixtures:
```
context 'with four live neighbours' do
    let(:live_cells) { build_list(:cell, 4) }

    it 'dies by overpopulation' do
        subject
        expect(cell.state).to eq(Cell::DEAD)
    end
end
```
So I texted a software developer friend 'I have immense love for fixtures in tests! So much easier and nicer to set things up with just few lines of code!'. But his response was 3 points of negativity:
    - But they hide complexity!
    - And make it more difficult if you need something slightly different.
    - Or the fixture end up being way too big so you can't handle it all at once.
    
    <br/>
    All three of which have some truth to it. But I'm still very happy with how the tests turned out:

    ![Specs](/assets/images/game_of_life_specs.jpeg){: width="375" 2rem;" }

<br/>
This has been a fun little exercise. I've done the majority of it in one evening, just finished adding specs, readme and general clean up later. Which gave me an ego boost, because I'm not sure if I had managed to do this so easily in one evening few years ago.