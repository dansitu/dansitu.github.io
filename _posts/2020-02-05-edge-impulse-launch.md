# Edge Impulse launch, TinyML and LoRaWAN

I just got home from an exciting week in Amsterdam. It was a big deal for a few reasons—the main one being that we announced the public launch of [Edge Impulse](http://edgeimpulse.com)! 🥳🍾

We've had a fantastic response so far; it already feels like a community is starting to grow around our product. It's been great hearing from all the people who have signed up and given it a try; here are a couple of my favorite reactions:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I have to admit I thought this demo was staged. After having tried <a href="https://twitter.com/EdgeImpulse?ref_src=twsrc%5Etfw">@edgeimpulse</a>, and ported it on <a href="https://twitter.com/hashtag/MXChip?src=hash&amp;ref_src=twsrc%5Etfw">#MXChip</a> over the weekend, I can only say that I&#39;m genuinely impressed. Awesome tool &amp; awesome UX <a href="https://twitter.com/hashtag/TinyML?src=hash&amp;ref_src=twsrc%5Etfw">#TinyML</a> <a href="https://twitter.com/hashtag/IoT?src=hash&amp;ref_src=twsrc%5Etfw">#IoT</a> <a href="https://t.co/ZnACuEpwTO">https://t.co/ZnACuEpwTO</a></p>&mdash; Benjamin Cabé (@kartben) <a href="https://twitter.com/kartben/status/1224382736514699264?ref_src=twsrc%5Etfw">February 3, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">How cool is that! I just created my first <a href="https://twitter.com/hashtag/MachineLearning?src=hash&amp;ref_src=twsrc%5Etfw">#MachineLearning</a> model and trained it within minutes, with no previous experience in <a href="https://twitter.com/hashtag/ML?src=hash&amp;ref_src=twsrc%5Etfw">#ML</a>. I’m really excited with <a href="https://twitter.com/EdgeImpulse?ref_src=twsrc%5Etfw">@EdgeImpulse</a> technology, countless <a href="https://twitter.com/hashtag/ML?src=hash&amp;ref_src=twsrc%5Etfw">#ML</a> applications in mind. Great job done ⁦<a href="https://twitter.com/janjongboom?ref_src=twsrc%5Etfw">@janjongboom</a>⁩ &amp; ⁦<a href="https://twitter.com/zach_shelby?ref_src=twsrc%5Etfw">@zach_shelby</a>⁩ ! <a href="https://t.co/6h80dBGuBN">pic.twitter.com/6h80dBGuBN</a></p>&mdash; Jaakko Ala-Paavola (@japikas) <a href="https://twitter.com/japikas/status/1224731746840739841?ref_src=twsrc%5Etfw">February 4, 2020</a></blockquote>

The product is genuinely amazing, though since I've only been at the company for a couple of weeks I can't take _too_ much credit! That said, I did get to build our epic sheep demo you can see in the video above.

### Meeting the team

The second exciting thing was meeting our whole team for the first time. Edge Impulse is a distributed company, and right now we’re split between Northern California and the Netherlands. It was my first time meeting CTO Jan Jongboom and ML infra engineer Mathijs Baaijens face-to-face, and it was great to get to know them a little better. I love remote work, but you can’t beat meeting people in person—there’s just much higher bandwidth for building relationships.

### LoRaWAN and TinyML

And _bandwidth_ brings me to my third topic. We announced our launch at [The Things Conference](https://www.thethingsnetwork.org/conference/), which I’d recommend for anyone interested in the embedded space. The conference is focused on [LoRaWAN](https://lora-alliance.org/about-lorawan), which is an extremely exciting set of technologies for long-distance, low-power radio communications. It’s hosted by [The Things Network](https://www.thethingsnetwork.org/), who provide tooling for devs building LoRaWAN systems.

If you haven’t heard of LoRaWAN, you should definitely take a look. LoRa-connected devices can make low data rate transmissions over long distances (potentially > 10km), using very little energy. The technology is designed for transmitting data from battery-operated sensors—think tiny environmental sensors that run for 5 years without battery replacement. Thanks to the WAN (_Wide Area Network_) part, these sensors can potentially report back through a global, distributed network of LoRa gateways run by various organizations.

One of the coolest technologies I saw at the conference was LoRa transmission to _space_. Companies like [Lacuna](https://lacuna.space/) and [Hiber](https://hiber.global/) are building satellite networks that allow LoRa-equipped sensors to transmit from anywhere on Earth. It’s now possible to transmit data from any location on the surface of the planet, and you can do it with a sensor that lasts 5 years on a tiny battery 🤯

LoRa is pretty magical, but due to regulations and power constraints it’s fundamentally a low-bandwidth channel. Connectivity is restricted to ~30 seconds of transmission per day, which in practice means you can only send a few bytes of data at a time, and no more than once every few minutes (on average). This is more than enough for many types of applications: think logging the current outdoor temperature, which doesn’t change very often, or reporting the GPS location of a slow-moving container ship.

However, some types of sensor data are just too bloated to send over LoRa. There’s no way to transmit meaningful amounts of audio, for example, and there’s not enough bandwidth to transmit the type of high frequency data generated by sensors like accelerometers.

This is where TinyML comes in. It often makes sense to view machine learning as a form of lossy compression: given a raw input, an ML model creates a representation of the same input that includes only the important information.

For an audio classification model with a binary output (perhaps “the machine sounds normal” vs. “the machine sounds faulty”), that could mean “compressing” a second of 44.1 kHz, 16-bit audio (88.2 kb) into a single bit. Clearly, it’s not possible to reconstruct the original audio sample from this—but that’s okay if the single bit contains all the information you care about.

This property makes TinyML the perfect partner to LoRaWAN networks, where bandwidth is at a premium. It allows whole new classes of sensors to be connected to LoRa networks—potentially from anywhere on the planet—in addition to enabling more intelligent use of available bandwidth with existing sensors, allowing them to only transmit when they genuinely need to.

Global networks of low-powered but intelligent sensors could transform our world and help us keep track of the things that we value the most. As a great example, [Smart Parks](https://www.smartparks.org/) are using solar powered and LoRaWAN-equipped sensors to monitor and protect wildlife, fighting back against poaching. It’s exciting to think of other ways these technologies can improve our world.

### Give Edge Impulse a try

Now that we've launched Edge Impulse, you can [sign up](http://edgeimpulse.com/) and try it out! The quickest way to get started is with an [STM32 IoT node discovery kit board](https://www.st.com/en/evaluation-tools/b-l475e-iot01a.html), which is about $50. You'll be able to capture audio and accelerometer data, and train classification models using classical ML and deep learning. It's super fun and easy—honestly, I was blown away the first time I saw it. If you do try the product, I'd love to hear what you think!

Warmly,

Dan
