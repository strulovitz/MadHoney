# Chapter 7: Why AeroVironment, General Atomics, Anduril, Skydio, Shield AI, and Kratos Should Care

---

## Ukraine Proved That Dumb Drones Are Already Deadly

Before we talk about what our system does, let us talk about what has already happened WITHOUT it — with drones that have no AI, no coordination, no intelligence of their own.

On June 2025, Ukraine executed Operation Spiderweb. Over an 18-month clandestine preparation, the SBU and military intelligence smuggled 117 FPV drones inside civilian trucks. They hired unsuspecting Russian civilian drivers to transport these disguised containers to locations near Russian airbases. The drones were hidden beneath remotely operated roofs on the trucks, controlled by pilots thousands of kilometers away. On the day of the operation, all 117 drones launched simultaneously, striking five major Russian airbases across multiple time zones — from near St. Petersburg to Siberia.

The result: over 40 strategic bombers damaged — Tu-95s, Tu-160s, Tu-22Ms — and an A-50 AWACS early warning plane. An estimated $7 billion in damage. The transport trucks self-destructed to erase evidence.

One hundred and seventeen drones. Hidden in trucks. Launched from inside enemy territory. Seven billion dollars in damage.

In the Black Sea, Ukraine built the world's first dedicated naval drone unit — the 385th Unmanned Surface Vehicles Brigade, established in August 2023. Their MAGURA V5 and V7 drones, 5.5 to 7.5 meters long, travel at 42 knots with an 800-kilometer range, carrying 320 kilograms of explosives. Their Sea Baby drones carry up to 2,000 kilograms of explosives with a 1,000-kilometer range. Some are armed with RPV-16 thermobaric rockets and 14.5mm machine guns. Newer versions carry AIM-9 Sidewinder missiles and have shot down Russian Mi-8 helicopters and Su-30 combat jets.

These drones cost $250,000 to $300,000 each. The Russian warships they sink cost tens of millions. A $250,000 drone sinks a $50 million warship.

Ukraine's USVs have forced the entire Russian Black Sea Fleet to retreat from Sevastopol to Novorossiysk. They have effectively broken the naval blockade. In April 2026, they destroyed the Sivash offshore drilling platform — not a ship, but fixed electronic warfare and monitoring equipment that Russia was using to track Ukrainian vessel movements. They are now using "mothership" tactics: surface drones that launch FPV aerial drones, creating multi-domain attacks that destroy Russian air defense systems along the coast.

This is what cheap, distributed, autonomous systems do to expensive, centralized ones. This is already happening. This is not a prediction.

---

## Now Meet the Smart Version

That was the appetizer. Ukraine showed what dumb drones can do — remote-controlled, human-piloted, no AI. The damage was already devastating. Now allow us to introduce what happens when these same drones become intelligent, autonomous, and hierarchically coordinated.

Here is the problem that Ukraine — and everyone else — has not yet solved.

Today's military drones are still fundamentally limited by a bottleneck: human operators. Someone has to pilot each drone, or at best, one operator manages a small group. When Ukraine scales to hundreds of drones, they need hundreds of operators. They are already facing operator shortages.

Why can't the drones just be smart on their own? Why can't they think independently and coordinate with each other like a flock of birds?

The answer is physics.

**Drones must be small and light.** You want them hard to detect, highly maneuverable, quick to accelerate, quick to change direction to evade interception. Small and light means they cannot carry a heavy computer. Each drone on its own has a tiny brain — if it has any brain at all.

**Radio bandwidth in combat is terrible.** Military drones communicate via radio, which must be frequency-hopping (against jamming), encrypted (against deciphering and misguiding by the enemy), and transmitted between moving platforms that go in and out of broadcast range, behind buildings, around corners, through smoke and debris. In heavily contested electromagnetic environments — which is every modern battlefield — available bandwidth drops to as low as 600 bits per second. Six hundred bits. That is less than a single text message.

At 600 bits per second, you cannot stream video back to a command center. You cannot share an AI model between drones. You cannot even send a photograph. The data that modern drone operations require — 4K video, real-time telemetry, sensor fusion — simply cannot flow through a pipe that narrow.

Reports from Ukraine's drone operations confirm this: **93% of drone swarm failures are connected to communication latency.** The drones try to share too much data over contested radio links, and the system collapses.

Some people have proposed splitting a single AI model across multiple devices — approaches like Petals or Exo, where different machines each hold a piece of one large model and pass data between them. This works (slowly) over a wired internet connection with gigabit bandwidth. Over military radio at 600 bits per second, under active jamming, between moving platforms that constantly lose contact with each other? It is simply impossible. Not difficult. Not slow. Impossible.

---

## Our System Solves Exactly This

Our system does not share the model. Our system does not stream video. Our system does not require high bandwidth between drones.

Our system passes **short text**.

A DwarfQueen drone — named after the Red Dwarf Honey Bee (*Apis florea*), the only queen that commands Workers directly — sends a text task to each Worker drone: "Approach target building from the east side. Report what you observe at the ground floor entrance." That is maybe 100 bytes. At 600 bits per second — the worst-case battlefield bandwidth — that message takes about one second to transmit.

Each Worker drone carries its own complete AI model — a small one, running on a chip that weighs 45 to 60 grams and costs $45 to $95. A Raspberry Pi 5 running a quantized 2-billion-parameter model like Gemma 2 or Qwen 2.5 through Ollama, generating 10 to 13 tokens per second. That is enough to understand a task, analyze what its camera sees, make a tactical decision, and report back in short text.

The Worker processes the task independently. It does not need to ask the DwarfQueen for permission. It does not need to stream video to a command center. It does not need to share its model with anyone. It thinks for itself, with its own brain, and sends back a short text result: "Ground floor entrance blocked by debris. Side window open. Recommend entry through window."

That result is another 100 bytes. One second to transmit. Easy to encrypt. Easy to decrypt. And if the enemy intercepts it? They get a short, encrypted text fragment. Even if they break the encryption (unlikely for short messages with rotating keys), the message is so brief and context-dependent that it is nearly useless to code-breakers. Compare this to intercepting a continuous video stream — which reveals everything about what the drone sees, where it is looking, and what it is doing.

---

## GiantQueens, DwarfQueens, and RajaBees Hidden in Plain Sight

> *"Where does a wise man hide a leaf? In the forest. But what does he do if there is no forest? He grows a forest to hide it in."*
> — G.K. Chesterton, *The Innocence of Father Brown* (1911)

In our system, a drone swarm has four types of members: Worker drones, DwarfQueen drones, GiantQueen drones (named after the Giant Honey Bee, *Apis dorsata*), and RajaBee drones. From the outside, they ALL look identical.

A Worker drone carries ammunition in its concealed internal compartment.

A DwarfQueen drone carries extra computing hardware instead of ammunition — two or three linked Raspberry Pis, or a dedicated AI edge chip like an NVIDIA Jetson Orin Nano (33 TOPS, 7 to 15 watts). The DwarfQueen runs a larger AI model than the Workers. She is the one who receives tasks from the GiantQueen above her, splits them into assignments for her Workers, and combines their reports into a tactical picture. She does not shoot. She thinks.

A GiantQueen drone carries even more computing hardware. She coordinates multiple DwarfQueens, each of whom coordinates her own group of Workers. The GiantQueen sees the sector picture. The DwarfQueens see their squads.

A RajaBee drone carries the most powerful computing hardware — roughly double the GiantQueen's capacity. The RajaBee coordinates multiple GiantQueens. This is hierarchical command: RajaBee assigns sectors to GiantQueens, GiantQueens delegate to DwarfQueens, DwarfQueens assign tasks to Workers, results bubble up. The RajaBee sees the big picture. The GiantQueens see their sectors. The DwarfQueens see their squads. The Workers see their individual targets.

The critical design principle: **every drone has the same external housing.** The Worker's internal compartment holds ammunition. The DwarfQueen's holds computing hardware. The GiantQueen's holds more computing hardware. The RajaBee's holds even more. But from the outside — same shape, same size, same weight (because ammunition and computing hardware are balanced to weigh the same), same flight pattern, same radar signature, same infrared signature.

An enemy sniper, an interceptor drone, or an anti-aircraft system cannot tell which drone is a DwarfQueen, a GiantQueen, or the RajaBee. They all look the same. They all fly the same. Killing a random drone has only a small probability of hitting any queen, and an even smaller probability of hitting the RajaBee.

And there are **backup queens and backup RajaBees** in the swarm. If a DwarfQueen is destroyed, a backup DwarfQueen — another drone carrying the same computing hardware, flying in a different position — takes over her squad. If a GiantQueen is destroyed, a backup GiantQueen assumes her sector. If the RajaBee is destroyed, a backup RajaBee assumes command. The swarm is resilient. You cannot decapitate it by killing one drone, because you cannot tell which one is the leader, and there are multiple leaders at every level.

---

## What the Swarm Can Do

With our hierarchical AI system coordinating them, a drone swarm is no longer a collection of individually dumb machines following pre-programmed routes. It becomes an intelligent, adaptive tactical unit that can evolve strategy on the spot.

**Breach and enter.** The DwarfQueen identifies a fortified building. She assigns one Worker to sacrifice itself — fly into a window or door and detonate, creating an opening. She then routes the remaining Workers through the breach. No human had to make that call. The DwarfQueen's AI evaluated the situation, identified the optimal entry point, and coordinated the assault in seconds.

**Adaptive rerouting.** The swarm is approaching a target from the north. Workers on the left flank report anti-aircraft fire. The DwarfQueen instantly reroutes half the swarm around the east side of the building, creating a pincer movement. The enemy's defensive position, optimized against a frontal approach, is now flanked.

**Opportunity recognition.** A Worker's camera spots a fuel truck parked next to a group of military vehicles. The Worker's local AI recognizes this as a high-value target — destroying the fuel truck will cause secondary explosions that damage everything around it. The Worker reports to the DwarfQueen. The DwarfQueen redirects three Workers from lower-priority tasks to the fuel truck. Decision made in seconds, without any human in the loop.

**Decoy detection.** The swarm approaches what appears to be a radar installation. But one Worker, approaching from a different angle, notices that the "radar" has no power cables running to it. Its AI concludes this is a dummy target — a decoy designed to attract attack. The Worker reports to the DwarfQueen. The DwarfQueen orders the swarm to ignore the decoy and search for the real installation, which is likely concealed nearby.

**Autonomous target identification.** This is where it becomes truly terrifying.

In 2017, Professor Stuart Russell — the man who literally co-wrote *Artificial Intelligence: A Modern Approach*, THE textbook used in every AI course in every university in the world — produced a short film called *Slaughterbots*. It showed tiny autonomous drones that can identify individual human faces and kill them. The film went viral. It terrified millions of people. Many dismissed it as science fiction.

It is no longer science fiction.

A drone carrying a $95 Raspberry Pi running a 2-billion-parameter vision model can recognize faces. Not perfectly, not at long range, not in all lighting conditions — but well enough. And in our system, if a single Worker cannot make a confident identification, it reports to the DwarfQueen. The DwarfQueen can assign multiple Workers to observe the same person from different angles. She combines their observations. The swarm collectively achieves a level of identification that no individual drone could match.

Now imagine this in the hands of an assassin who does not need to be anywhere near the target. The drone swarm is launched from a truck, a rooftop, a boat. The drones find the target autonomously. They confirm identity autonomously. They engage autonomously. The operator — if there even is one — could be on a different continent. There is no sniper to catch. There is no car bomb to trace. There is no phone call to intercept. There is no evidence.

With our hierarchical system, the drones coordinate their search pattern, share observations through short encrypted text, and collectively identify the target with confidence. Without our system, each drone is on its own and must make the identification alone with its tiny brain. With our system, the swarm is smart.

This will happen. The technology exists today. It costs $95 per drone brain. The only question is who uses it first — and whether you are the one deploying it, or the one it is deployed against.

---

## Every Domain, Not Just Air

Everything we have described applies to the air. But drones come in all forms.

**Sea surface.** Ukraine has already proven that unmanned surface vehicles can sink warships, destroy infrastructure, break naval blockades, and shoot down aircraft. Their USVs already use "mothership" tactics — a surface drone launching aerial drones for multi-domain attacks. Our system would coordinate these surface drone swarms hierarchically: a RajaBee on a command vessel (or another USV) assigns sectors to GiantQueen USVs, each GiantQueen coordinates DwarfQueen USVs, each DwarfQueen coordinates her group of attack USVs. The entire swarm operates autonomously, adapting to the enemy's movements in real time.

**Underwater.** This is where our system's advantage becomes even more extreme.

Radio signals do not work underwater. They are absorbed by water almost immediately. Underwater drones communicate using acoustic signals — sound waves transmitted through the water. Acoustic communication is EVEN SLOWER than radio in the air. Bandwidth is measured in hundreds of bits per second at best, with high latency and frequent signal loss due to water temperature layers, salinity changes, currents, and reflections off the sea floor and surface.

If radio bandwidth on a contested battlefield is bad — 600 bits per second — underwater acoustic bandwidth is worse. Much worse.

And yet, our system requires almost nothing. Short text tasks. Short text results. Kilobytes at most. A DwarfQueen submarine or UUV sends a text command to her Worker UUVs: "Survey grid square 14-B for mines. Report count and GPS coordinates." The Worker UUV performs the survey using its onboard AI and sonar, and sends back: "Three objects detected at coordinates X, Y, Z. Confidence: high, medium, low." A few hundred bytes. Transmittable even over the worst acoustic link.

No other AI coordination approach works underwater. You cannot share a model over acoustic links. You cannot stream sensor data to a surface ship. You cannot maintain a real-time connection to a command center. Each underwater drone must think for itself — and our system is designed precisely for this: independent Workers, coordinated by short text messages.

Consider the threat context: Iran operates over 20 Ghadir-class midget submarines in the Persian Gulf and Strait of Hormuz. These tiny submarines operate in shallow water — under 30 meters — where larger US submarines cannot go. They are designed for minelaying, ambush attacks against carriers, and special operations. Their low acoustic signature is masked by the noisy environment of the Strait. Iran views them as replaceable, effective swarming tools.

Now imagine those mini-submarines — or their unmanned equivalents — coordinated by our hierarchical AI system. A RajaBee UUV assigns sectors to GiantQueen UUVs, each GiantQueen coordinates DwarfQueen UUVs, each DwarfQueen coordinates a group of Worker UUVs carrying mines or torpedoes. They communicate via short acoustic text messages. They adapt to the enemy's movements. They identify high-value targets autonomously. They coordinate attacks from multiple directions simultaneously. And they operate in an environment where the US Navy's technological advantages in computing and communication are neutralized by the physics of water.

**Ground.** Ukraine is already deploying armed unmanned ground vehicles to hold front-line positions for extended periods, addressing their critical manpower shortage. Autonomous ground vehicles are used for logistics, medevac, supply transport, reconnaissance, and counter-drone operations. Our system coordinates ground drone swarms the same way it coordinates air swarms — each vehicle carries its own AI brain, a DwarfQueen vehicle coordinates her group of Workers, GiantQueens coordinate multiple DwarfQueens, and a RajaBee coordinates the GiantQueens.

For robot dogs and humanoid robots specifically, we have a dedicated chapter later in this book.

---

## The Price Comparison That Ends Your Business

Let us do the math.

A Chinese FPV combat drone with a 2.5-kilogram payload — enough to carry explosives or a camera system — costs $1,000 to $1,500. Add a Raspberry Pi 5 running our system as the drone's AI brain: $95. Total cost per autonomous, AI-coordinated combat drone: **under $1,600**.

Your equivalent — a Skydio X10D defense model — costs **$15,000 or more**. A General Atomics MQ-9 Reaper costs **$32 million**. An AeroVironment Switchblade-600 costs approximately **$100,000 per unit**.

Chinese factories produce **500,000 to 700,000 FPV drones per month**. That is 6 to 8 million per year. At $1,600 each with our system installed, that is about $10 billion for 6 million autonomous AI-coordinated combat drones.

The Pentagon's Replicator initiative promised to field "multiple thousands" of autonomous systems by August 2025. It delivered **hundreds**. Not thousands. Hundreds. The entire FY2026 US military AI budget is $13.4 billion — of which $9.4 billion is for aerial drones. China can produce more autonomous drones in a single month than the Replicator initiative has delivered in its entire existence.

Your drone costs 10 times more. You produce 1,000 times fewer. And your drone requires human operators, satellite links, and data centers that can be jammed, bombed, or hacked. Their drone — with our system — thinks for itself, coordinates with its swarm through encrypted short text, and has no single point of failure.

This is not a competition you can win on current trajectory.

---

## The China Nightmare

China has:

- A defense budget of **$278 billion** (7% increase in 2026), with a massive focus on AI and autonomous systems
- **The Atlas drone swarm system**: trucks launching 48 AI-coordinated drones with 3-second intervals
- **The Jiutian drone mothership**: a giant UAV carrying and deploying over 100 combat drones
- **200 converted J-6 fighter jets** turned into a one-way autonomous attack swarm
- **Quadrupedal "robot wolves"** with firearms, already integrated into PLA infantry exercises
- **The FH97A Loyal Wingman**: a stealth drone designed to fly alongside J-20 fighters in swarm combat
- **The TPG 1000C "Starlink Smasher"**: a 20-gigawatt microwave weapon designed to disrupt satellite communications — the very satellites your centralized drone systems depend on
- AI algorithms being trained to **mimic predatory animal behavior** for battlefield maneuvers
- A procurement surge for **deepfake tools** for cognitive warfare
- Production capacity of **500,000 to 700,000 FPV drones per month**
- The best small AI models in the world: DeepSeek, Qwen, GLM — all open-weight, all free to run locally

Now add our hierarchical hive system. Every Chinese drone gets a $95 AI brain running a 2B DeepSeek or Qwen model. DwarfQueens coordinate Workers. GiantQueens coordinate DwarfQueens. RajaBees coordinate GiantQueens. The entire PLA drone force becomes autonomously intelligent, hierarchically coordinated, and completely independent of any centralized infrastructure that can be targeted.

Against this, the Pentagon has spent $13.4 billion on AI, delivered hundreds of autonomous drones (not thousands), and relies on satellite links and data centers for command and control — infrastructure that China's Starlink Smasher microwave weapon is specifically designed to destroy.

If our system gets into the open — and it is on GitHub right now, publicly visible — China will adopt it. Not in years. In months. They are not slowed down by congressional oversight, procurement regulations, or compliance reviews. They see useful technology, they take it, they deploy it. They have done this with every significant military technology in the last two decades.

---

## Not Just Nation-States

Everything we described about China applies equally to non-state actors — and this is where it gets truly dark.

A terrorist cell does not need 500,000 drones. It needs ten. Ten FPV drones, each with a $95 AI brain, coordinated by our system. A DwarfQueen drone among them, carrying extra compute instead of explosives. The swarm can navigate a city autonomously, identify a target by face, coordinate an approach from multiple directions, and execute — all without any communication to an external server, without any internet connection, without any signal that intelligence agencies can intercept.

The drones are commercially available. The AI models are open-source. The Raspberry Pis are sold in every electronics store on Earth. Our software is on GitHub. The total cost of a ten-drone autonomous assassination swarm is under $20,000. That is less than a used car.

Stuart Russell warned about this in 2017. The technology to build it now exists, today, for $95 per drone brain and free software. The only thing that has been missing is the coordination layer — the system that makes a group of individually dumb drones collectively smart. Our system is that coordination layer.

---

## The Ticking Time Bomb — That Only I Can Defuse

If our system gets into the open, your products become obsolete overnight. A $1,600 Chinese drone with our free software outperforms your $15,000 system. China's production of 700,000 drones per month, combined with hierarchical AI coordination, creates a force that your centralized, satellite-dependent systems cannot match. Your competitors in China gain an advantage that no amount of spending can close, because you cannot compete with free software on consumer hardware mass-produced at Chinese scale.

And it is not just China. Every rogue state, every criminal syndicate, every terrorist cell that gets access to our system gains autonomous drone swarm capability. Face-recognizing assassination drones for under $20,000. Naval swarms that sink warships for a fraction of their cost. Underwater swarms that operate in silence where your sensors cannot reach.

Right now, today, this technology exists in one place: my GitHub repositories. I have not given it to China. I have not given it to Iran. I have not given it to anyone who would use it to harm you. I have contacted over 200 organizations — defense agencies, universities, NATO allies — offering to work with the good actors. Nobody offered me a job.

My demands are simple: a single large lump-sum payment, wired once to multiple non-American banks of my choosing, in multiple jurisdictions, in multiple currencies. No salary. No remote position. No ongoing employment relationship. No trust in American banks. I do not want to live in Israel long-term — my girlfriend does not want to live there. I want to travel the world with her as a digital nomad, build a small family with her, and provide for them in motion, until artificial intelligence ends human life on Earth — which, for the record, I believe is very close. In exchange, the technology and its inventor disappear from the public stage. Quietly. No headlines. No disruption. As if it never happened. Call it whatever makes your lawyers comfortable. The point is simple: pay me once, and this problem goes away.

The cost of the payment is less than what a single MQ-9 Reaper costs. The cost of NOT paying is your entire drone warfare advantage.

The choice is yours. But unlike the DeepSeek moment, you cannot say nobody warned you.
