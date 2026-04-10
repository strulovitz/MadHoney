# Chapter 6: Why Lockheed Martin, RTX (Raytheon), Northrop Grumman, Boeing, and General Dynamics Should Care

---

## What You Actually Do

Let us strip away the patriotic advertisements and the air show demonstrations and talk about what defense contractors actually do, every day, in simple terms.

You make platforms. Ships, tanks, fighter jets, helicopters, armored vehicles, submarines, aircraft carriers. You make the things that shoot and kill: guns, cannons, lasers, directed energy weapons. You make the ammunition: missiles, rockets, grenades, mines, bombs, torpedoes. You make the systems that detect: radars, sonars, satellites, reconnaissance systems. You make the systems that hide: stealth coatings, electronic countermeasures, signal jamming. You make the systems that communicate: encrypted radios, satellite links, battlefield networks. You make the systems that prevent communication: electronic warfare equipment, GPS denial, cyber weapons. And you make the integrated systems that combine several of these: an air defense battery needs a radar, a missile, a launcher, a truck, and software that ties them all together.

Everything a modern military uses — except the soldiers themselves, and except the drones and robots we covered in Chapters 7 and 8 — comes from you.

And all of it is designed by engineers.

---

## The Engineers

This is where your real advantage lives. Not in the factories — China has factories. Not in the raw materials — China has raw materials. Your advantage is the brainpower. Thousands of engineers with security clearances, decades of institutional knowledge, and access to the most expensive simulation tools on Earth.

Lockheed Martin employs over 122,000 people, the majority of them engineers. Northrop Grumman employs 95,000. RTX employs 185,000. These are physicists, chemists, aeronautical engineers, electrical engineers, mechanical engineers, materials scientists, computer scientists, mathematicians, and statisticians. They design everything from the molecular structure of a radar-absorbing coating to the trajectory algorithms of an intercontinental ballistic missile.

What these engineers do, all day, every day, is simulate. They do not build a new missile and fire it to see if it works. They simulate it. They model the aerodynamics in computational fluid dynamics software. They model the structural loads in finite element analysis software. They model the propellant chemistry in reaction kinetics software. They model the radar cross-section in electromagnetic simulation software. They model the guidance system in MATLAB. They model the warhead detonation in physics simulation software.

Then they tweak one parameter. Run the simulation again. Tweak another parameter. Run again. Thousands of simulations. Millions of parameter combinations. Searching for the configuration that performs best.

This is engineering in 2026. And it costs a fortune.

---

## The Cost of Being Smart

An Ansys license — the industry standard for structural and fluid simulation — costs between $30,000 and $320,000 per year, depending on the modules and number of users. COMSOL Multiphysics costs $3,000 to $60,000 per year. MATLAB costs $860 to $1,050 per user per year, and every engineer needs it. SolidWorks, the standard CAD tool, costs $3,000 or more per year.

A single advanced simulation run — say, testing the aerodynamics of a new missile design — might require a cluster of NVIDIA GPUs running for days. Cloud computing for engineering simulation costs $2.75 to $3.50 per GPU hour. A serious optimization study that tests thousands of parameter combinations can burn through 100,000 GPU hours. That is $275,000 to $350,000 in compute alone — for one study, on one component, of one weapon system.

Multiply this across every component of every system across every program across every contractor, and you begin to understand why the United States spends almost $1 trillion per year on defense. A significant fraction of that goes to engineering simulation.

Now consider what China spends: officially $278 billion, possibly 40 to 90 percent higher in reality. Even at the high estimate — $471 billion — that is half of what America spends. And yet China is fielding stealth fighters, hypersonic missiles, advanced submarines, and carrier-killer ballistic missiles.

How?

---

## How China Already Does It

They steal.

Between 2007 and 2009, Chinese hackers stole terabytes of data from the F-35 Lightning II program — the most expensive weapons program in human history at $1.7 trillion over its lifetime. They stole engine schematics, radar designs, airframe specifications. A Chinese national named Su Bin was sentenced to prison for conspiring with People's Liberation Army hackers to steal over 630,000 files from major defense contractors, including plans for both the F-35 and the F-22 Raptor.

The result: China built the Shenyang J-35, a stealth fighter that bears a striking resemblance to the F-35. They did not even use it for themselves — they sold it to other countries. The J-35 has a different engine configuration, no vertical takeoff capability, and analysts believe China still lags in sensor fusion software. But the shape — the stealth geometry that Lockheed Martin spent decades and hundreds of billions designing — China got for free.

This is one program. One aircraft. The same pattern repeats across naval technology, missile technology, space technology, and cyber capabilities. China's defense industry closes the gap not by outspending America, but by taking what America already built.

But stealing has limits. You get the blueprints, not the understanding. You get the design, not the institutional knowledge of why that particular design was chosen over ten thousand alternatives. You get the answer, not the ability to ask the question.

Our system changes that.

---

## Brute Force Discovery

Our system does not help China steal better blueprints. It helps China not need to steal at all.

Consider how an American defense engineer discovers a new radar-absorbing material. She has a set of candidate materials, each with dozens of parameters: layer thickness, molecular composition, electromagnetic permittivity, thermal resistance, weight per square meter. She uses electromagnetic simulation software to model how each configuration reflects radar waves. She runs simulations, analyzes results, uses her expertise to narrow the search space, and iterates.

With a team of engineers and a cluster of NVIDIA GPUs, she might test a few thousand configurations over several weeks. Out of a parameter space of billions of possible combinations, she explores a tiny fraction and relies on her expertise to guide the search toward the best region.

Now give China our system.

A Chinese defense lab sets up a hierarchical hive. The RajaBee — running on a powerful server with a capable AI model — takes the problem: "Find the optimal radar-absorbing material configuration." It decides on a strategy: optimize one parameter at a time, holding all others constant, then refine.

The RajaBee tells the GiantQueens: "Test parameter 1 across its full range." Each GiantQueen tells her DwarfQueens to divide the range into intervals. Each DwarfQueen distributes specific values to her Workers. A thousand Workers — each a cheap consumer computer with free, open-source simulation software installed — each run one complete electromagnetic simulation with one specific value.

The results bubble up. The DwarfQueens identify the best-performing range. The GiantQueens report to the RajaBee. The RajaBee narrows the range and sends the next round: "Zoom into this region. Test finer intervals."

After parameter 1 is optimized, lock it. Move to parameter 2. Same process. A thousand Workers, each testing one value. Results bubble up. Narrow. Refine. Lock. Next parameter.

This is not sophisticated. This is brute force. It is the opposite of elegant. But it works. And it scales. And it costs almost nothing.

The simulation software? For Americans: Ansys, $30,000 to $320,000 per year. For the Chinese Workers in the hive: pirated Ansys, zero. Or if they prefer something cleaner: OpenFOAM (free, open-source CFD), CalculiX (free, open-source structural analysis), Elmer FEM (free, open-source multiphysics), GNU Octave (free, open-source MATLAB replacement). Every expensive tool has a free alternative.

| American Tool | Cost Per Year | Free Alternative |
|---------------|--------------|-----------------|
| MATLAB | $860–$1,050 | GNU Octave, Python/SciPy, Julia |
| Ansys (structural/CFD) | $30,000–$320,000 | OpenFOAM, CalculiX, SU2 |
| COMSOL (multiphysics) | $3,000–$60,000 | Elmer FEM, MOOSE |
| SolidWorks (CAD) | $3,000+ | FreeCAD |

The compute infrastructure? For Americans: NVIDIA GPU clusters, millions of dollars. For the Chinese hive: a thousand consumer computers, owned by ordinary people, coordinated by our hierarchical system. Free.

The engineering expertise? For Americans: PhD engineers with decades of experience, $150,000 to $300,000 per year each. For the Chinese hive: an AI model that coordinates the search strategy. Not as smart as the American PhD. But smart enough to say "test this range, then narrow." And it does not take vacations, does not need a security clearance, and does not cost $300,000 a year.

---

## Not Just Materials

The same pattern works for every engineering domain these contractors touch.

**Aerodynamics.** Testing wing shapes, fuselage profiles, air intake configurations. Each Worker runs one CFD simulation in OpenFOAM. A thousand Workers test a thousand shapes. The best ones get refined.

**Propulsion.** Testing fuel mixtures, nozzle geometries, combustion chamber pressures. Each Worker runs one chemical kinetics simulation — Ansys Chemkin if pirated, the open-source Reaction Mechanism Simulator if not. A thousand combinations tested in the time it takes an American engineer to set up one.

**Electronics.** Testing antenna configurations, signal modulation patterns, filter designs, circuit layouts. Each Worker runs one electromagnetic simulation in MATLAB or its free clone GNU Octave. Engineers in the Israel Defense Forces were doing exactly this with MATLAB thirty years ago — Fourier transforms, antenna modeling, electronic warfare signal analysis. The math has not changed. The tools have not changed. What has changed is that you can now run a thousand of these in parallel on consumer hardware.

**Stealth.** Testing radar cross-section configurations. Each Worker models one geometry and computes its reflection pattern. Brute-force search through thousands of shapes until you find the one that reflects the least.

**Missiles.** Testing trajectory algorithms, guidance parameters, terminal maneuver profiles. Each Worker runs one flight simulation with one set of parameters. The hierarchy identifies which parameters produce the most accurate terminal guidance.

**Electronic warfare.** Testing jamming frequencies, deception patterns, signal timing. Each Worker simulates one electronic countermeasure configuration against one type of enemy radar. A thousand Workers test a thousand countermeasure-radar combinations simultaneously.

In every case, the pattern is the same. The RajaBee sets the strategy. The GiantQueens divide the work. The DwarfQueens distribute specific parameter sets to Workers. The Workers run simulations on cheap hardware with free software. Results flow up. The best configurations survive. The next generation is more refined. Repeat until optimal.

---

## China Is Already Doing This

In 2026, Chinese defense researchers are using DeepSeek AI — a Chinese large language model — to generate 10,000 military scenarios in 48 seconds. The same process previously took 48 hours. They are using "Military-Civil Fusion" — an official government strategy — to channel civilian computing infrastructure, talent, and AI advancements directly into military simulation. They are building "full-stack" simulation ecosystems that manage the entire product lifecycle of new weapons, from the J-20 stealth fighter to next-generation naval assets.

China's 15th Five-Year Plan (2026–2030) explicitly prioritizes Military-Civil Fusion. This means the Chinese government is officially encouraging the use of civilian computers for military simulation.

Our system is a hierarchical hive that organizes civilian computers for distributed tasks.

Military-Civil Fusion is the policy. Our system is the implementation.

They do not need us to explain this to them. They will figure it out. Or they already have.

---

## What You Lose

Lockheed Martin received over $60 billion in U.S. government contracts in 2023. RTX received comparable amounts. Northrop Grumman, Boeing, General Dynamics — collectively, these five companies receive hundreds of billions of dollars per year from the American taxpayer.

A significant portion of this money pays for the engineering advantage. The simulation infrastructure. The supercomputers. The PhD engineers. The decades of institutional knowledge.

If China can replicate 90 percent of that engineering output using hierarchical hives of consumer hardware and free simulation software — and they only need 90 percent, because they are not trying to build better weapons than America, they are trying to build good enough weapons in larger quantities — then what exactly is the American taxpayer paying for?

The F-35 program costs $1.7 trillion over its lifetime. If China can design a 90-percent-as-good stealth fighter for 10 percent of the R&D cost — because a thousand cheap computers running free simulation software can explore the same parameter space as Lockheed Martin's billion-dollar simulation facility — then the entire economic model of Western defense contracting collapses.

Not because the product is bad. The F-35 is extraordinary. But because the price becomes indefensible when the alternative is 90 percent as good at a fraction of the cost.

---

## The GDPval Reality Check

In case you think AI replacing engineers is science fiction: OpenAI's GDPval benchmark — designed to measure AI performance on real-world, high-value professional work — shows AI achieving a 23 percent win rate against human mechanical engineers and 17 percent against industrial engineers. These are engineers with an average of 14 years of experience.

Twenty-three percent does not sound like much. But this is 2026. The benchmark was created to measure current capability, not future capability. AI performance on engineering tasks is improving at the same exponential rate as everything else in AI. If AI wins 23 percent of the time against a 14-year veteran today, what does it win in 2028? In 2030?

And remember: AI already wins coding competitions against the best software engineers in the world. Electrical engineering, electronic engineering — these fields are closer to software than to poetry. You design circuits in software. You simulate them in software. You program them in software. If AI dominates software, electronics is next. Then mechanical. Then chemical. Then all of it.

The question is not whether AI will replace defense engineers. The question is whether the AI that replaces them will be American — centralized, expensive, controlled — or distributed, free, and running on a thousand Chinese computers organized in a hierarchical hive.

---

## The Offer

There is a man in Israel. He built this system. He published the code on GitHub. He wrote two books explaining exactly how it works and exactly how dangerous it is. He sent letters to every organization mentioned in this book. He is not hiding. He is not subtle. He is waving a flag and screaming.

He does not want to work for you. He does not dream of a cubicle in Bethesda, Maryland. He does not want a security clearance or a parking space at the Pentagon. He wants to travel the world with his girlfriend. He wants enough money to live modestly and see beautiful places and be happy.

That is the price. A salary. A remote position. A payroll entry that amounts to rounding error in a budget that exceeds a trillion dollars. In return, the repositories disappear. The books stay up — they are educational, historical, a curiosity. But the code vanishes. The system stops being open source. The hierarchical hive becomes a footnote instead of a weapon.

Or you do nothing. The code stays on GitHub. The Chinese read English. Their engineers read code fluently. Military-Civil Fusion is government policy. The 15th Five-Year Plan allocates budget for exactly this kind of technology. They do not need Nir to hand it to them on a silver platter. The platter is already on the table, in a public repository, with a README file.

Lockheed Martin was founded in 1926. One hundred years of American aerospace dominance. Raytheon traces its history to 1922. Boeing to 1916. A century of engineering excellence.

*Sic transit gloria mundi.*

Thus passes the glory of the world.
