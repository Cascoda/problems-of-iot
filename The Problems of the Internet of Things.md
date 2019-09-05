# The Problems with the Internet of Things

At Cascoda, we have been working on IoT radio chips for over a decade.
This gives us a unique window into what we believe are the fundamental
problems with the Internet of Things.

## The Internet of Things is Proprietary

The current state of IoT protocols is quite messy. There are numerous
solutions for connecting IoT devices to each other and to the cloud.
Unfortunately, the vast majority of these solutions involve completely
different proprietary stacks which cannot natively talk to each other, or
to the Internet.

There are essentially two options for building a connected home today:

-   Choose one "walled garden" and stay within it. Devices within a
    manufacturer's closed platform will work well together, but you are
    locked into that ecosystem. If a competitor launches a novel,
    desirable product, you cannot use it unless you ...

-   Run different IoT networks within your home. This is very
    inconvenient and most people don't want to do this. And in most
    scenarios the different networks cannot even talk to each other,
    making the home a lot less "connected" than is ideal.

Contrast this with the way the World Wide Web works: by using open
standards, devices from different manufacturers can talk using the
Internet Protocol, even using completely different communication stacks.
For instance, a Samsung phone can access a web page using its mobile
network (GSM/LTE) just as well as an ASUS laptop can over Wi-Fi, or a
Dell PC over Ethernet.

To ensure its survival and widespread adoption, the Internet of Things
must abandon walled gardens and vendor lock-in, in favour of open
standards and interoperability.

## The Radio Range is Insufficient

Most people understand the capabilities and limitations of Wi-Fi, and
expect IoT devices to behave in a similar fashion. However, it is very
difficult to reach the range of Wi-Fi while maintaining a useful data
rate without consuming significant power. For instance, [smartphones
expend significant amounts of energy powering their
radios](https://www.usenix.org/legacy/event/atc10/tech/full_papers/Carroll.pdf),
and they must be recharged daily. This would be unacceptable
for the Internet of Things.

Anybody who has tried to set up any sort of non-trivial IoT network has
run into this issue. It is very difficult to create a network which
covers the entire house without relying on a plethora of gateways and
routers, which significantly increases complexity and cost.

The UK Office of Communications concluded that [2.4GHz IoT solutions
can only cover 36% of UK
houses](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/486058/Ofcom_Smart_Meter_HAN_868MHz_RF_Coverage_Campaign.pdf).
And using longer range sub-gigahertz radio (433MHz worldwide, 868MHz in Europe and
915MHz in North America) comes with its own set of issues, such as
limited bandwidth, no global frequency allocation, and no support for
native IP connectivity.

## IoT Security has become a [Joke](https://xkcd.com/2166/)

We don't believe IoT security is being taken seriously enough. Countless
IoT vulnerabilities are being exposed every year. For instance, [the
Bluetooth Low Energy smart-lock which can be remotely cracked in two
seconds](https://www.pentestpartners.com/security-blog/totally-pwning-the-tapplock-smart-lock/).
All you need to know to open that lock is the BLE MAC address, which is
publicly broadcasted. The lock can even be defeated with a trivial
[replay
attack](https://en.wikipedia.org/wiki/Replay_attack).

There is also the case of the [hair straightener which can be accessed
by anyone within Bluetooth
range](https://www.pentestpartners.com/security-blog/burning-down-the-house-with-iot/):
The device does not use any sort of authentication - and could even set
your house on fire.

The largest DDOS attack on record [took advantage of compromised IoT
devices](https://www.csoonline.com/article/3258748/the-mirai-botnet-explained-how-teen-scammers-and-cctv-cameras-almost-brought-down-the-internet.html),
hosted by [almost 50,000 unique IPs spread across 164
countries](https://www.imperva.com/blog/malware-analysis-mirai-ddos-botnet/).
You would think that such a successful attack would use highly
sophisticated ways of cracking each device. That couldn't be further
from the truth: [Mirai hijacked over 500,000 IoT devices by using a
list of 60 default
credentials](https://www.grahamcluley.com/mirai-botnet-password/).
And although the Mirai botnet is old news by now, [variants of this
attack are still being
deployed](https://unit42.paloaltonetworks.com/new-mirai-variant-adds-8-new-exploits-targets-additional-iot-devices/).

IoT security is a complex, multifaceted issue. Security can fail at any
point within the technology stack. There is little you can do to guard
against devices being insecure at the application level, other than
attempt to minimize damage to the rest of the network.

## How can we fix it?

We believe we have a solution which solves these problems. The solution
consists of SMARTRange, our innovative wireless transceiver
architecture, coupled with Thread, an IoT protocol based on IPv6.

### Cascoda & SMARTRange

We have been working on a solution for the range problem since 2007, and we
are now bringing it into production. We have invented [a new type of radio
demodulator](https://www.cascoda.com/innovation/) which offers a significant
increase by improving receiver sensitivity. The upside of our approach is
that the increase in range is obtained without sacrificing power consumption
and with no need for a power amplifier. This significantly reduces deployment
and production costs.

In our open-space tests, we have achieved [radio communications at a
range of over 900
metres](https://www.kickstarter.com/projects/imgtec/creator-ci40-the-ultimate-iot-in-a-box-dev-kit/posts/1585703).
Independent [tests within a dense urban
environment](https://www.innovelec.co.uk/manufacturers/cascoda/case-studies/ca-8210-range-tests)
show the Cascoda radio outperforming a long-range Bluetooth radio, a
proprietary 868MHz radio and residential Wi-Fi. From outside, we were
even able to achieve communications with an in-door device from 235
metres away.

[Our latest module, the Chili 2](https://www.cascoda.com/chili2/), comes with a microcontroller featuring [ARM TrustZone
technology](https://developer.arm.com/ip-products/security-ip/trustzone),
which provides hardware-level isolation of secure code and data. This
allows the developer to, for instance, store the network key in a way
which is completely inaccessible to application-level software,
preventing a buggy or otherwise compromised application from leaking
security credentials.

Cascoda provides all the tools necessary to implement state-of-the-art
IoT security. Since we are a vendor of IoT radios, we have limited
influence over how our customers implement application-level security.
However, we make it very easy to integrate our devices with the latest
communication stacks which aim to be secure by default.

We are also committed to open-source software. Our [source development
kit](https://github.com/Cascoda/cascoda-sdk) is available on GitHub, [our
driver is part of the Linux
tree](https://github.com/torvalds/linux/blob/master/drivers/net/ieee802154/ca8210.c)
and we are [a contributor to the open-source Thread stack,
OpenThread](https://github.com/openthread/openthread#who-supports-openthread).

### Thread

Thread is one of the most open IoT stacks. The [specification is
available free of
charge](https://www.threadgroup.org/ThreadSpec). And, as mentioned above, Google Nest has released
[OpenThread, the open-source implementation of
Thread](https://github.com/openthread/openthread).

Thread is [built on open
standards](https://www.threadgroup.org/news-events/blog/ID/112/Why-Thread-Chose-IPv6),
mirroring the structure of the Internet in the hopes of becoming
ubiquitous. A big advantage of Thread is that it is
application-layer agnostic: [many different application layers can run
on the same
network](https://www.threadgroup.org/news-events/blog/ID/187/Like-Wi-Fi-for-the-IoT-How-being-application-agnostic-sets-Thread-apart-from-the-rest).
This is not possible with ZigBee or Z-Wave, where you'd have to run an
entirely separate network for every different application layer. Thread
also makes interoperability between different manufacturers simpler:
companies and engineers are already familiar with the Internet Protocol.

The protocol takes advantage of IPv6 to allow any device on a Thread
network to talk to the World Wide Web. Usually, you can only talk to
your IoT gateway over the web, and then tell it to control its children.
Thread simplifies all of that and lets you directly talk to any child
via its IPv6 address, if it is desirable to do so.

Thread also takes a strong stance on security: unlike other protocols
such as Bluetooth Low Energy, you cannot create an unsecured Thread
network, you must have the correct credentials to talk to any Thread
network, and all communications are encrypted. [Thread uses
standardized and well-established security
protocols](https://www.threadgroup.org/news-events/blog/ID/109/PART-TWO-Securing-the-Connected-Home-From-Outside-Threats),
minimizing the chance of an attacker being able to breach the network's
security.

Additionally, the Thread Group has developed a [commissioning
app](https://openthread.io/guides/border-router/external-commissioning#download-the-thread-commissioning-app)
which is the easiest and most secure way of adding a new device to a
Thread network. This minimizes the risk of application developers
deploying non-secure commissioning processes, or relying on \[widely
known\] default passwords.

## Conclusions

IoT adoption is being slowed down by lack of standardization and the
prevalence of proprietary protocols. The industry must embrace open
standards if it wants to match the success of the Internet. The use of
walled gardens and vendor lock-in, combined with insufficient radio
range, makes deployment of complex IoT networks prohibitively expensive.

Cascoda embraces open standards and software through our open-source SDK
and endorsement of Thread, the open IoT stack. Our SMARTRange radio
architecture has double the range of existing technology without
sacrificing power consumption. We also take a strong stance on security
by supporting protocols which are secure by default, as well as offering
support for the latest tools for embedded software security.
