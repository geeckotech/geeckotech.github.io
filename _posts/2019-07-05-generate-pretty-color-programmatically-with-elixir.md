---
layout: post
title:  "Randomize pretty color programmatically with elixir"
date:   2019-07-05 00:18:23 +0700
author: "VirKill"
categories: [elixir]
---

> Abstract: How to programmatically randomize beautiful compatible color? This is a basic approach but can easily extended once the concept is grasped. The implementation is written in elixir but can be applied in any language.

In one of your project, you might encounter situation where you want to randomize color for background, variety of text, ect. One way to do it of course is just to provide it with an array of predefined options. Such as :

{% highlight elixir %}
    Enum.random(["#F46036", "#5B85AA", "#414770", "#372248", "#171123"])
{% endhighlight %}

The example above randomize a list of hex color. Other than hex format, CSS understand RGB, and [css color code](https://www.w3schools.com/cssref/css_colors.asp). None of it can easily be manipulated programmatically other than using random function over predefined list.

## Introducing HSV color system

There are other format called HSV (Hue, Saturation, Value). Here's how it worked:

![Alt text](/static/img/hsv.png "HSV")

- <b>Hue (H)</b> is represented as degree in color wheel, so it can have range from 1 to 359.

- <b>Saturation (S)</b> is how 'washed' it is, with range from 1 to 100 (percentage).

- <b>Value (V)</b> is how light or dark it is, with range from 1 to 100 (percentage).

Using this [tool](https://www.rapidtables.com/convert/color/hsv-to-rgb.html) for example we can get the idea on how HSV can be easily converted into RGB or hex on the fly .

<img src="/static/img/hsv-rgb-converter.png"  style="max-width:400px;">

Reading the HSV to RGB spesification from wikipedia [(https://en.wikipedia.org/wiki/HSL_and_HSV)](https://en.wikipedia.org/wiki/HSL_and_HSV) we can make a function to convert HSV into RGB, and RGB to hex.

{% highlight elixir %}
defmodule Color do

  def hsv_to_rgb(%{hue: hue, saturation: saturation, value: value} = _hsv) do
    h = hue / 60
    i = Float.floor(h) |> trunc()
    f = h - i

    sat_dec = saturation / 100

    p = value * (1 - sat_dec)
    q = value * (1 - sat_dec * f)
    t = value * (1 - sat_dec * (1 - f))

    p_rgb = get_rgb_color(p)
    v_rgb = get_rgb_color(value)
    t_rgb = get_rgb_color(t)
    q_rgb = get_rgb_color(q)

    case i do
      0 -> %{red: v_rgb, green: t_rgb, blue: p_rgb}
      1 -> %{red: q_rgb, green: v_rgb, blue: p_rgb}
      2 -> %{red: p_rgb, green: v_rgb, blue: t_rgb}
      3 -> %{red: p_rgb, green: q_rgb, blue: v_rgb}
      4 -> %{red: t_rgb, green: p_rgb, blue: v_rgb}
      _ -> %{red: v_rgb, green: p_rgb, blue: q_rgb}
    end
  end

  def rgb_to_hex(%{red: red, green: green, blue: blue} = rgb) do
    hex =
      ((1 <<< 24) + (red <<< 16) + (green <<< 8) + blue)
      |> Integer.to_string(16)
      |> String.slice(1..1500)

    "#" <> hex
  end

  defp get_rgb_color(color) do
    (color * 255 / 100) |> trunc()
  end  

  def hsv_to_hex(h,s,v) do
    hsv_to_rgb(%{hue: h, saturation: s, value: v}) |> rgb_to_hex
  end

end
{% endhighlight %}

Now we can just call `hsv_to_hex(h,s,v)` funtion to get the hex color.

> Back to the question ` how we can randomly generate compatible color programmatically?`. The trick is just to set fixed Saturation and Value and randomize the Hue.

For example, set fixed Saturation to 50 and Value to 90 and randomize the H will produce something similar like this:

![Alt text](/static/img/random-color.png "HSV")


There we have it! A pretty color randomizer function. In the next article we can turn this function into an SVG Initial based avatar generator.
