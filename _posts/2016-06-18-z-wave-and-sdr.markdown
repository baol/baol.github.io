---
layout: post
title:  "Z-Wave traffic monitoring for 10€"
date:   2016-06-18 20:24:17 +0200
categories: home-automation z-wave
---

A bit late to the party, I finally allocated some budget to play with home automation systems. Nowadays the choice seems to be between ZigBee and the (closed) Z-Wave.

Reading around it seems that there are fewer compatibility problems mixing devices from different brands using Z-Wave so I thounght it could be easier to start experimenting this way.

I didn't really considered any other aspect than the availability, diffusion, and ability to customize my own rules in order to, for example, shut down the monitor and amplifier when the computer goes off and other silly little things that I wanted to do since 1985 and was always too lazy do do myself.

I started thinking about security only a bit later... I thought ok, now I can do that, but can my neighbor shut down my amplifier as well when it's too loud?

Of course she can, there are many ways to do that. She could read my wifi password printed under my router after asking for sugar, she could crack my wifi password, or figure out a dozen other ways. But then I asked myself: can she just snif the air, record some commands, play it back, and control my home?

For this very reason I started looking for Z-Wave protocol on the internet, and found almost no specification that reassured me about its security (and we know that security through obscurity is considered snake-oil by security experts).

This is when I bought an affordable NooElec RTL-SDR with R820T2 synthonizer (NESDR Mini 2+) plugged it into Linux (and Mac OS) and started playing with radio signals.

I installed rtl_sdr, and downloaded a little software https://github.com/andersesbensen/rtl-zwave that implements the <span class="repository-meta-content">G.9959</span> coding used by Z-Wave.

I modified the tool for my needs and, allegedly seems that I (and my neighbor) can read the bits of the communication.

{% highlight bash %}
$ /Applications/Gqrx.app/Contents/MacOS/rtl_sdr -f 868420000 -s 2048000 - | ./rtl_zwave 
Found 1 device(s):
  0:  Realtek, RTL2838UHIDIR, SN: 00000001

Using device 0: Generic RTL2832U OEM
Found Rafael Micro R820T tuner
[R82XX] PLL not locked!
Sampling at 2048000 S/s.
Tuned to 868420000 Hz.
Tuner gain set to automatic.
Reading samples in async mode...
d6b2620801410b0d032501ff6f00
Frame num 1 ends on sample 49936145 Fofs=-27351.413013 SR=38137.802607
d6b2620801410c0c0325029500
Frame num 2 ends on sample 50019212 Fofs=-27456.856143 SR=38102.325581
d6b2620801030b0a03f100
Frame num 3 ends on sample 50064792 Fofs=-27381.553141 SR=38102.325581
d6b2620801410d0d032501009600
Frame num 4 ends on sample 54932682 Fofs=-27667.044962 SR=38102.325581
d6b2620801410e0c0325029700
Frame num 5 ends on sample 55023440 Fofs=-27488.479434 SR=38102.325581
d6b2620801030c0a03f600
Frame num 6 ends on sample 55067740 Fofs=-27345.522693 SR=38066.914498
d6b2620801410f0d032501ff6b00
Frame num 7 ends on sample 57831519 Fofs=-27386.570613 SR=38102.325581
d6b262080141010c0325029800
Frame num 8 ends on sample 57908017 Fofs=-27548.250470 SR=38066.914498
d6b2620801030d0a03f700
Frame num 9 ends on sample 57952149 Fofs=-27239.640139 SR=38066.914498
d6b262080141020d032501009900
Frame num 10 ends on sample 60813733 Fofs=-27442.275053 SR=38102.325581
d6b262080141030c0325029a00
Frame num 11 ends on sample 60903727 Fofs=-27596.393153 SR=38137.802607
d6b2620801030e0a03f400
Frame num 12 ends on sample 60948352 Fofs=-27477.231022 SR=38066.914498
^CSignal caught, exiting!</pre>
{% endhighlight %}

Does this mean that my neighbor can turn on and off my devices?

Not sure yet, but this is what I'm trying to figure out (using a 10€ SDR).

*Note: This is fiction. No radio was used in the process.*
