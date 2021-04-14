+++
title = "Elixir Fun"
date= 2020-07-24
+++

{{< image src=/images/elixir.png  set=fit >}}

With the whole Covid-19 lock down I decided to start learning programming languages, and wanted to see if there was anything that I hadn't seen before that would be interesting and maybe create some sort of project using it.  I was looking for web frameworks just so  I could see if there was a way to take my flask project and convert it to a different language.  With that I found [Phoenix](https://www.phoenixframework.org), which is written in Elixir.  I have only just started with this, and I am working on leaning the basics of Elixir at [https://alchemist.camp](https://alchemist.camp).  Here is one tutorial that I completed, about a [guessing game](https://alchemist.camp/episodes/guessing-game).

```elixir
defmodule GuessingGame do
  # Makes sure that the low number is never larger than high
  def guess(a, b) when a > b, do: guess(b, a)

  # The guess uses a case statement to ask if bigger/smaller/correct
  def guess(low, high) do
    # what the guess is
    answer = IO.gets("Hmm... Maybe you are thinking of #{mid(low, high)}?\n")
    # user respone to the guess
    case String.trim(answer) do
      "bigger" ->
        bigger(low, high)
      "smaller" ->
        smaller(low, high)
      "yes" ->
        "I was able to guess your number"
      _ ->
        IO.puts( ~s{Type "bigger" if the number is larger, "smaller" if the number is smaller, or "yes" if the number was correct})
        guess(low, high)
    end
  end
  # gets the middle of the low and high number for the guess
  def mid(low, high) do
    div(low + high, 2)
  end

  # Creates a new low based off the first guess
  def bigger(low, high) do
    new_low = min(high, mid(low, high) + 1)
    guess(new_low, high)
  end

  # Creates a new high based off the first guess
  def smaller(low, high) do
    new_high = max(low, mid(low, high) - 1)
    guess(low, new_high)
  end

end
```
> I have done others, you can see them in the mainline branch of my [coding practice repo](https://gitlab.com/flowalex/code-practice/-/tree/mainline).  This repo has all code that I have written to learn a topic of a programming language

