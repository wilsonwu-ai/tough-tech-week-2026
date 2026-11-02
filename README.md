# Short on Data, Not on Brains: What MIT's Physical-AI Day Said, and What I Could Check

*By Wilson Wu. Recorded at MIT on October 30, 2026, during Tough Tech Week.*

**The short answer.** Physical AI, meaning software that senses and acts in the real world through robots, wearables and machines, is short on physical-world training data and on reliability, not on intelligence. That was the thread through the nine sessions I recorded at Imagination in Action's physical-AI summit at MIT. General models get a robot most of the way; the last stretch needs the customer's own data, and customers want failure rates today's demos do not reach. Some speakers expect computing to move toward the device, though most of it still runs in the cloud, and power draw is the harder wall. Money is plentiful, and a panel said it is pooled in a few very large rounds (a share I could not verify). The talk that stayed with me was about design: build machines that make people matter more. As an operator-investor, apparel-brand owner and computer science student, my takeaway is this: durable businesses sit one layer away from the robot (data, integration, service, components), and for clothing, sensing beats actuation for now.

---

## The day in context

The summit ran at the MIT Samberg Conference Center on Friday, October 30. I recorded nine sessions on my phone across three stages: Machine Perception [1], Fuel for Physical AI [2], Show, Don't Code [3], Colin Angle's keynote Coming Home [4], Daniela Rus in A Matter of Trust [5], The Physical AI Stack [6], Soft and Wearable Robots [7], Raising an Early Round [8], and Neil Gershenfeld's Frontiers of Physical AI [9]. Most recordings have no speaker labels, so I name a speaker only where the attribution is clear.

The policy backdrop moved the same month. The White House issued a proclamation adjusting imports of robotics and industrial machinery, calling them essential to nearly all modern manufacturing [10]. A Mayer Brown client note points out that it "does not impose tariffs yet" [11].

---

## 1. Data is the fuel; who owns it is the fight

The most repeated claim of the day came from Michael Healy of LabyrinthAI, which turns human demonstrations into robot training data. A general vision-language-action model (a VLA: one network that takes camera images plus an instruction and outputs motor commands) "will get you maybe 80 to 90% of the way there," he said. The rest takes data from the customer's own factory [2]. On Show, Don't Code the same idea arrived as a recipe: start from a pretrained VLA, improve it with reinforcement learning (training by trial and reward), then fine-tune on site data [3].

Investors treated data as the diligence question. Enja Ahearn of AWS Corporate Development said she asks founders where their proprietary data came from, because many products are thin wrappers around someone else's language model [2]. Chase Olle of Robot on Rails noted how little footage of ordinary lab work, such as pipetting, exists online [2]. Robin Walters of Braid Robotics said a human can learn a task in one to three demonstrations, and claimed his models are two to three orders of magnitude more data-efficient [3]; I found no paper behind that.

On Raising an Early Round, one investor (likely Hyperplane's, attribution inferred) called proprietary data, customer integration and the team the real moat, and a panelist said labs now come asking to buy startups' data. One panelist's board is debating it: "do we sell the data to the labs?" [8]

What I could check:
- Bessemer Venture Partners: "Data is expensive, capital is the moat." [12]
- OpenVLA, an open 7-billion-parameter model, beat the closed 55-billion-parameter RT-2-X by 16.5% in absolute task success across 29 tasks, per its authors [13]. That supports pretrain-then-fine-tune, though no paper I found backs the 80 to 90% figure.
- An attendee's LinkedIn recap relayed a figure attributed to Sangbae Kim: about 425 million hours of training data for autonomous driving versus under 1 million for robot manipulation [14]. I did not record that session; treat it as secondhand.
- Against all this, one X post quips that for startups generally "There is no moat . You are defenseless and also can win it" [15], and a Hacker News commenter says many robot demos are built for that one demo [16].

My read: the data argument holds, but the data that lasts is the byproduct of a robot already doing paid work.

---

## 2. 99% is the product

Romeo Catracchia of AutonomUS, which builds an AI-guided ultrasound robot for procedures such as nerve blocks, told the clearest reliability story. A robot can be very precise and still succeed only 50% of the time, he said, while his target is north of 99%; learning the tricks of experienced clinicians closed much of that gap. Matching humans is not enough, he argued: a device must beat clinicians to be worth buying, with the clinician kept in the loop as the basis of trust [2].

On Show, Don't Code, a panelist relayed a manufacturer's verdict on an end-to-end model: "When I tried this model, it was 90% reliable." That was a rejection. The startup moved its AI to a higher layer above a conventional robot interface and trains in simulation [3]. Massimiliano Versace of Analog Devices described robotics as a graveyard of failed companies and said survival takes extreme reliability plus a sharp first application [6]. Online practitioners are harsher: one Hacker News commenter wrote that "even 95% success rate is not enough for factory/logistics automation if the failure is unrecoverable" [17].

Daniela Rus, director of MIT CSAIL, argued that wiring a language model straight to a robot has limits because the model carries no model of the physical world. She criticized training first and adding guardrails (filters that block unsafe outputs) later, since guardrails can be stripped off. She wants safety specified mathematically and trained in, so a model is safe "in a way that's very difficult to undo" [5]. Trust, she said, grows through experience plus objective measures such as miles driven without a human stepping in, and autonomy should start where machines already beat people, like the port trucks of Venti Technologies, which she co-founded, parking within a few centimeters for a crane [5].

The research cuts both ways. RoboPAIR's authors call it the first algorithm built to jailbreak (trick into unsafe behavior) robots run by language models [18], echoing a jailbreak story told, garbled on my recording, at Show, Don't Code [3]. Yet RoboGuard, a runtime guardrail added on top, cut how often unsafe plans were carried out from over 92% to under 3% in its authors' tests [19]. That is the bolt-on approach Rus criticized, working well in a lab. The live question is where the safety layer sits, not whether a robot needs one.

---

## 3. Beyond the RGB camera

The Machine Perception panel argued that ordinary color cameras are not enough. MIT researcher Ashley Neall said single-photon sensors (chips that count individual particles of light, useful for depth and for seeing around corners) now cost around $60 to $70, where optical-bench setups once ran about half a million dollars. She predicted cheap sensors like these will support much better 3D reconstruction for robots within five years. The bottleneck now is resolution, not cost, and existing image datasets do not carry over, so she is building an open-source platform for collecting this data [1]. A panelist, likely Ubicept's Tristan Swedish, added that a fixed sensor caps what you can learn: train only on internet photos and you inherit the cameras that took them [1].

Three more points from that panel [1]:
- Touch is missing from the standard robot stack, even though people handle objects by feel.
- A synthetic-data practitioner found that variety in lighting, angles and scenes mattered more than photorealism, because models grab shortcuts.
- Physics, not pixels, is the hard part. A robot cannot practice 100 years of picking up bags of Skittles, and simulators struggle with a bag that lags the arm and tears.

One panelist summed up simulated data beyond visible light: "We don't have a great answer for everything across the EM spectrum." [1] Rus added that new sensors change which algorithms work; MIT's ground-penetrating radar maps soil under the road, which does not change with the weather [5].

What I could check: the 2017 domain-randomization paper, which trains on deliberately varied simulations, is the published root of the diversity-over-realism lesson [20]. Photon-level methods exist in research, including burst vision [21] and radiance fields trained on individual photons [22]. ForceVLA, which adds force sensing to a VLA, reported a 23.2% average gain in task success over strong baselines [23], though force sensing is not skin-like touch.

---

## 4. The power wall

The Physical AI Stack panel held the day's sharpest disagreement. Moderator Dave Blundin of Link Ventures framed a $7 trillion AI infrastructure build-out and claimed at least half of it is wasted, and probably 90% or more [6]. Vijay Gadepally of MIT Lincoln Laboratory said software alone has doubled throughput inside some customers' data centers, letting companies defer hundreds of millions of dollars of capital spending [6].

Ramesh Raskar of the MIT Media Lab argued for the edge, meaning models that run on the device rather than in a data center. "I think AI is going to be more like electricity than oil," he said: many small producers instead of a few big ones. He predicted the shift within three months and suggested 99.9% of people could use AI models offline. Gadepally called three months aggressive; today, he said, about 99% runs in the cloud and 0.1% at the edge [6]. Rus described a hybrid, local-first future, citing Liquid AI's small on-device models [5].

Power is the harder limit. Versace said robots need a million-fold cut in power draw to run for hours instead of minutes [6]. On the wearables panel, a panelist said the personalization models are small and run on the device's own controller [7].

What I could check:
- The liquid-network lineage is real: closed-form continuous-time networks claim training and inference one to five orders of magnitude faster [24], and neural circuit policies are peer-reviewed [25]. Liquid AI's own LFM2 report claims prefill and decode run up to twice as fast on CPUs as similarly sized models [26].
- Edge hardware is shipping. NVIDIA, a vendor, claims Jetson Thor offers up to 7.5 times the AI compute and 3.5 times the energy efficiency of the previous Jetson generation [27]. AMD, also a vendor, lists a 15 to 54 watt range for its embedded Ryzen AI parts [28].
- Not everyone buys it: one Hacker News commenter argued on-device computing pays off only in narrow cases [29].

Gershenfeld's Center for Bits and Atoms went after the energy floor itself [9]. He framed an eight-order-of-magnitude gap between how well we compute and how well we fabricate. Jake Read showed sensor-laden machine tools that plan their own jobs. Erik Strand showed interlocking 3D compute tiles that, he said, beat an NVIDIA H200 on some operations. Camron Blackburn presented superconducting logic (AQFP circuits cooled near absolute zero), claiming about 100x lower energy per device even after cooling and about 15x across a full system [9]. AQFP papers describe the logic family as extremely energy efficient [30], but I found no independent check of those system numbers. Gershenfeld's line: "the code doesn't describe the thing, the code becomes the thing." [9]

---

## 5. Follow the money

The moderator of Raising an Early Round opened with physical-AI funding above $47 billion this year and said most of it went to the top ten companies, so early-stage founders rarely see the headline dollars [8]. As I heard the panel:
- How long a technical lead protects a company has shrunk to between 18 months and three years.
- Overvalued: rounds raised on demos, horizontal general-purpose robotics, capital-heavy healthcare robotics, and paid human data collection.
- Underloved: energy, hazardous work, agriculture, and plain tasks like deburring. One panelist cited a parking-lot customer paying $57,000 a month for manual sweeping versus $6,000 with robots.
- Advice: ship a product that is roughly 10% okay, buy generic parts, and build only what nobody else has solved.

Those are panel claims I could not verify. What I could:
- Crunchbase counts $47.4 billion across 521 physical-AI deals in the first half of 2026 [31], and $18.8 billion raised by robotics startups so far in 2026, against $15 billion in all of 2025 [32].
- Defense News, citing PitchBook, reported a record $49.1 billion for defense-tech startups in 2025, a count that includes dual-use companies [33]. That matches the panel's story of a snow-removal robotics startup being pulled toward defense [8].
- Yahoo Finance reported Figure valued at $39 billion [34]. The roboticist Rodney Brooks tells humanoid investors: "You’re wasting your money." [35]
- Gasgoo, covering Unitree's IPO approval amid tougher profit pressure, reported its pure humanoid shipments topped 5,500 units in a year [36].
- Transport Topics reported UPS will invest $120 million in 400 truck-unloading robots [37]. The International Federation of Robotics ties US robot demand to a lasting shortage of skilled labor [38].

My read as an investor: robot hardware is getting cheaper and more crowded, so margin moves toward software, data, service and integration. The pattern I would underwrite looks like the UPS order: an enterprise buyer, a defined task, a payback period you can model. That is how I think about it, not investment advice.

---

## 6. Augment, don't replace

Colin Angle, co-founder of iRobot, has shipped 15 million robots [4]. Roomba, he noted, is about 25 years old and is still basically a Roomba, and he expects roughly another such cycle before physical AI changes most people's lives. He once believed the perfect robot is one you never see or touch, and he was wrong: 90% of owners named their Roomba, moved chairs to help it, and wanted a relationship with it [4].

A garden that grows itself, he argued, repeats that mistake; growers want a pet tractor that helps them do the growing they love. A robot that cooks for a frail grandmother takes away how she shows love; a better one helps her keep cooking. His three tests: does it need me, does it know me, can it carry my care? He closed: "The goal, after all, is to enable human connection, not replace it." [4]

The same rule surfaced elsewhere. AutonomUS keeps the clinician in the loop [2]. The wearables panel caps assistance so the wearer can always overpower it [7]. Online, a consultancy's recap recast Angle's invisible-Roomba versus helpful-Roomba slide as a design rule for AI products generally [39].

---

## Soft wearables and apparel

Assistive wearables are real where someone pays for a measurable pain. Smart clothing keeps failing on washing, power and apps.

**Worker suits are the proof point.** A Soft and Wearable Robots panelist described warehouse workers moving about a thousand boxes a day in a soft suit taking 40% of the strain off the back; both the line and the company name were garbled on my recording [7]. Separately, TechCrunch reported Verve Motion's claim that its worker exosuit (a soft, powered garment that assists the body) cuts back strain by up to 30 to 40% [40], a vendor figure. The panel also named adoption friction: a nurse may transfer a patient 12 times a day, too often to keep putting a device on and off [7].

**Personalization is the technical lever.** A panelist described tuning by asking the wearer, over and over on a phone or watch, which of two assistance profiles feels better [7]. Harvard reported that pairing its exosuit with a tuning algorithm cut the energy cost of walking by 17.4% versus no device [41]. A 2022 Nature paper showed such tuning can happen quickly in real-world conditions [42], and Harvard engineers note that one fixed controller can help one wearer and hinder the next [43].

**Consumer devices avoid the medical label.** Moderator Hiawatha Bray of the Boston Globe said people at one exoskeleton company asked him not to depict their device as medical or rehabilitative, "because they were terrified of being pushed into having to get licensed by the FDA." He added that people with walking disabilities buy Hypershell, which is marketed as recreational [7]. The FDA's general-wellness policy covers low-risk products that promote a healthy lifestyle [44]; I could not confirm that any maker relies on it. Nike says more than 400 athletes logged over 2.4 million steps in its Project Amplify powered-footwear program [45]. The clinical route runs through licensing: Harvard licensed its lower-extremity soft exosuit technology to ReWalk [46], and a 2019 Textile World report called ReWalk's ReStore the only soft exo-suit with FDA clearance at that time [47]. Hacker News commenters add that cost held back approved rehab exoskeletons [48], and that the payoff is stamina, not productivity [49].

**Smart apparel stalls on the basics.** In early Los Angeles store sales, three Levi's and Google Jacquard jackets were the only ones sold in the first two hours, per 9to5Google [50], and Google ended Jacquard support on April 24, 2023 [51]. E-textiles lose some performance with every wash [52]. Anything with a radio needs FCC authorization before it can be marketed [53]. Each added battery, radio and app is another way to fail.

**Where an apparel brand fits.** Sensing is the apparel-compatible entry point; actuation is not, yet. A Llume panelist described stretchable fiber-optic sensors that capture breathing and impacts with one sensor where several synchronized ones used to be needed [7]. Myant sells washable, stretchable textiles for healthcare, automotive and industrial uses and offers contract manufacturing of textile computing solutions [54]. Loomia lists flexible heaters [55]. Moving fabrics are still lab work, such as the MIT Media Lab's electrofluidic fiber muscles for robots and wearables [56].

The capital-light path is co-development. In 2022, Cornell's news office covered a campus collaboration with Organic Robotics, then led by Ilayda Samilgil, who appeared on the Soft and Wearable Robots panel as CEO of Llume (I could not verify that Llume is the renamed Organic Robotics); the founders hoped one more year of trials would get them to production [57]. MIT's Self-Assembly Lab developed the heat-activated yarn in a 4D-knit dress made with Boston's Ministry of Supply [58]. In both, the lab carried the R&D and the brand carried fit, production and customers.

For my own brand, the order I am weighing: partner first (sensing or heated pieces built on a supplier's certified module that work with no app, or garments designed around worker suits, an untested idea until suit makers say they want it); co-develop a small capsule with a lab second; own hardware IP last, which I am parking. Any wellness or safety claim on a label needs a lawyer's review first.

---

## Ten predictions to check by 2030

These are predictions, not findings. Rows 1 to 7 are my forecasts: rows 1 to 3 are my own judgment with no source behind them, and rows 4 to 7 cite the source that prompted them. Rows 8 to 10 are speaker predictions.

| Prediction | Signal that confirms | Signal that falsifies |
|---|---|---|
| 1. Horizontal robot foundation-model companies stay private and hard to value through 2028 | No pure-play robot-model IPO and no large disclosed revenue by end of 2028 | One lists or discloses large recurring revenue |
| 2. Physical-AI funding stays concentrated in a few mega-rounds | Crunchbase's 2027 and 2028 tallies again show a handful of deals taking a large share | Deal counts grow broadly with no round dominating |
| 3. Humanoid hardware prices and margins keep falling | Unitree and peers report lower prices and gross margins in filings | Margins stabilize or rise with volume |
| 4. The US follows the October 2026 proclamation with a tariff or quota on robots or parts [10][11] | A tariff or quota action by end of 2027 | A negotiated deal replaces tariffs, or nothing happens |
| 5. Payback-led deployments scale to thousands of units per customer [37] | Orders like UPS's move from hundreds to thousands of units | Large pilots stall at hundreds |
| 6. US robot installations keep growing on labor shortages [38] | IFR's US counts rise in most years through 2030 | Two straight years of decline |
| 7. Massachusetts funds robotics, but its share of national robotics venture money does not rise [59][60][61] | State money is enacted while the state's share stays flat | The state's share rises clearly |
| 8. Speaker (Neall): cheap single-photon sensors enable robot-grade 3D reconstruction within five years [1] | Large public single-photon datasets; robots shipping with these sensors | Still lab-only by 2030 |
| 9. Speaker (Raskar, disputed by Gadepally): a meaningful share of AI moves to the edge [6] | Robot makers run core control on embedded modules like Thor or Ryzen AI [27][28] | Flagship robots still depend on cloud calls for core tasks |
| 10. Speaker (Angle): broad consumer impact takes roughly another 25-year cycle [4] | Powered apparel and consumer exoskeletons stay niche; Nike's powered footwear has no broad launch [45] | A powered garment or shoe sells at mainstream apparel volumes |

Context for row 7: Mintz summarized a state plan with $100 million for defense innovation [59], a Boston Globe source said "Billions are invested somewhere else" [60], and MassTech counts $733.9 million of venture capital in Massachusetts robotics across 2022 and 2023 [61].

---

## What I didn't hear and couldn't verify

**What I missed.** I did not record the sessions with Russ Tedrake, Sangbae Kim or Pulkit Agrawal, so I know them only through attendee recaps [14]. Most of my recordings start a few minutes into the session. Transcription mangled many names (Rhoda AI came out as RERDA, Llume as Loon), which I corrected only against the published schedule.

**Claims I am holding back until I find a primary source:**
- Rus's 90-neuron network that drives a car [5]. The published work I found is the neural circuit policies line [25], and I could not confirm the neuron count.
- The 40% back-strain figure from the wearables panel [7]. The closest checkable number is a vendor's "up to 30 to 40%" [40], and I could not confirm which company the panelist meant.
- Blundin's $7 trillion and its wasted share, Versace's million-fold, Blackburn's 15x and Strand's H200 comparison [6][9].
- The top-ten funding share, the parking-lot savings, a claimed 10 to 12 times multiple for subscription revenue, and startup revenue figures garbled on the recording [8].
- Braid's two-to-three-orders-of-magnitude data-efficiency claim [3], Neall's sensor prices [1], and the $500 to $700 consumer exoskeleton prices mentioned on the wearables panel [7].
- The secondhand 425 million versus 1 million hours figure [14].
- A Hacker News mention of an Arc'teryx mobility exoskeleton, which the commenter was unsure would become a real product [62].

I did not read Reddit, and X had almost nothing on the event itself.

---

## How this was made

I recorded nine sessions on my phone from the audience and transcribed them locally with Whisper, an open-source speech-to-text model. No audio was shared or uploaded. AI research agents then checked the claims against academic papers, social posts and industry sources, with a separate pass on soft wearables. Every quote here was string-matched in code against the transcripts, or against the live or saved source page (a few matches were partial). Web sources whose quoted text could not be found were dropped, along with any number resting only on them. Where a recording had no speaker labels, I named a speaker only when context made it clear; otherwise I wrote "a panelist". Transcription errors inside quotes are left as spoken. Nothing here is investment, legal or medical advice.

---

## References

1. Session recording: Machine Perception, Oct 30 2026
2. Session recording: Fuel for Physical AI, Oct 30 2026
3. Session recording: Show, Don't Code, Oct 30 2026
4. Session recording: Coming Home (Colin Angle keynote), Oct 30 2026
5. Session recording: A Matter of Trust (Daniela Rus), Oct 30 2026
6. Session recording: The Physical AI Stack, Oct 30 2026
7. Session recording: Soft and Wearable Robots, Oct 30 2026
8. Session recording: Raising an Early Round, Oct 30 2026
9. Session recording: Frontiers of Physical AI, Oct 30 2026
10. White House fact sheet on adjusting imports of robotics and industrial machinery: https://www.whitehouse.gov/fact-sheets/2026/10/fact-sheet-president-donald-j-trump-adjusts-imports-of-robotics-industrial-machinery-and-their-parts-and-components-into-the-united-states/
11. Mayer Brown, proclamation on imports of robotics and industrial machinery: https://www.mayerbrown.com/de/insights/publications/2026/10/president-trump-issues-proclamation-on-imports-of-robotics-industrial-machinery-and-their-parts-and-components
12. Bessemer Venture Partners, robotics and physical AI predictions: https://bvp.com/atlas/bessemer-predicts-robotics-and-physical-ai
13. OpenVLA (arXiv 2406.09246): https://arxiv.org/abs/2406.09246
14. Attendee LinkedIn recap of the summit (search results page): https://www.linkedin.com/search/results/content/?keywords=Imagination%20in%20Action%20MIT%20physical%20AI&sortBy=%22date_posted%22
15. Eno Reyes on X: https://x.com/EnoReyes/status/2109540083284267356
16. Hacker News comment on robot demos: https://news.ycombinator.com/item?id=49112627
17. Hacker News comment on VLA reliability: https://news.ycombinator.com/item?id=49964758
18. RoboPAIR (arXiv 2410.13691): https://arxiv.org/abs/2410.13691
19. RoboGuard (arXiv 2503.07885): https://arxiv.org/abs/2503.07885
20. Domain randomization (arXiv 1703.06907): https://arxiv.org/abs/1703.06907
21. Burst Vision Using Single-Photon Cameras (WACV 2023): https://openaccess.thecvf.com/content/WACV2023/html/Ma_Burst_Vision_Using_Single-Photon_Cameras_WACV_2023_paper.html
22. Radiance fields from single-photon cameras (arXiv 2407.09386): https://arxiv.org/abs/2407.09386
23. ForceVLA (arXiv 2505.22159): https://arxiv.org/abs/2505.22159
24. Closed-form continuous-time networks (arXiv 2106.13898): https://arxiv.org/abs/2106.13898
25. Neural circuit policies enabling auditable autonomy: https://research-explorer.ista.ac.at/record/8679
26. LFM2 technical report (arXiv 2511.23404): https://arxiv.org/abs/2511.23404
27. NVIDIA Jetson Thor availability (Robotics Tomorrow): https://www.roboticstomorrow.com/news/2025/08/25/nvidia-blackwell-powered-jetson-thor-now-available-accelerating-the-age-of-general-robotics/25415/
28. AMD Ryzen AI embedded processors at CES 2026 (Robotics 24/7): https://www.robotics247.com/article/ces-2026-amd-introduces-ryzen-ai-embedded-processor-portfolio/amd
29. Hacker News comment on edge computing: https://news.ycombinator.com/item?id=49673188
30. AQFP superconducting logic (arXiv 2309.12212): https://arxiv.org/abs/2309.12212
31. Crunchbase News, physical AI funding in H1 2026: https://news.crunchbase.com/venture/physical-ai-funding-startups-robotics-aerospace-h1-2026/
32. Crunchbase News, robotics startup funding in 2026: https://news.crunchbase.com/robotics/startup-venture-funding-surges-2026-data/
33. Defense News, defense tech funding in 2025: https://www.defensenews.com/industry/2026/01/20/defense-tech-startups-had-their-best-funding-year-ever-in-2025/
34. Yahoo Finance, Figure valuation: https://finance.yahoo.com/news/figure-valued-39-billion-latest-131115237.html
35. TechCrunch, Rodney Brooks on humanoid robots: https://techcrunch.com/2025/09/26/famed-roboticist-says-humanoid-robot-bubble-is-doomed-to-burst
36. Gasgoo, Unitree IPO approval: https://autonews.gasgoo.com/articles/ICV/unitree-wins-ipo-approval-as-robot-makers-face-tougher-profit-challenges-2061816669448765440
37. Transport Topics, UPS truck-unloading robots: https://www.ttnews.com/article/ups-robots-unload-trucks
38. International Federation of Robotics, US robot industry growth: https://ifr.org/news/us-robot-industry-returns-to-double-digit-growth/1
39. Consultancy LinkedIn post on the Angle keynote (search results page): https://www.linkedin.com/search/results/content/?keywords=Imagination%20in%20Action%20MIT%20physical%20AI&sortBy=%22date_posted%22
40. TechCrunch, Verve Motion exosuit: https://techcrunch.com/2021/07/15/verve-motion-raises-15m-following-exosuit-pilot-with-grocery-workers
41. Harvard Gazette, exosuit improvement: https://news.harvard.edu/gazette/story/2018/02/exosuit-improvement
42. Slade et al., personalizing exoskeleton assistance in the real world (Nature): https://doi.org/10.1038/s41586-022-05191-1
43. Harvard SEAS, AI and assistive wearables: https://seas.harvard.edu/news/can-ai-make-wearable-technologies-and-assistive-devices-more-helpful
44. FDA, general wellness policy for low-risk devices: https://www.fda.gov/regulatory-information/search-fda-guidance-documents/general-wellness-policy-low-risk-devices
45. Nike, Project Amplify: https://about.nike.com/en-GB/newsroom/releases/nike-unveils-project-amplify-the-worlds-first-powered-footwear-system-for-running-and-walking
46. Wyss Institute, soft exosuit: https://wyss.harvard.edu/technology/soft-exosuit
47. Textile World, FDA clearance for the ReStore exo-suit: https://www.textileworld.com/textile-world/nonwovens-technical-textiles/2019/06/fda-issues-clearance-for-the-restore-exo-suit-the-first-soft-robotic-system-for-stroke-therapy/
48. Hacker News comment on rehab exoskeleton cost: https://news.ycombinator.com/item?id=50015315
49. Hacker News comment on exoskeletons and endurance: https://news.ycombinator.com/item?id=50026447
50. 9to5Google, early Jacquard jacket sales: https://9to5google.com/2017/09/27/google-and-levis-sold-just-3-jacquard-enabled-jackets-in-the-first-2-hours-of-sales-in-la/
51. 9to5Google, Jacquard app shutdown: https://9to5google.com/2023/03/28/google-shutting-down-jacquard-app/
52. Fashnerd on e-textiles and washing: https://fashnerd.com/?p=31631
53. 47 CFR 15.101, equipment authorization: https://www.law.cornell.edu/cfr/text/47/15.101
54. Myant: https://www.myant.ca
55. Loomia: https://www.loomia.com
56. MIT Media Lab: https://www.media.mit.edu/
57. Cornell Chronicle, wearable sensor startup collaboration: https://news.cornell.edu/stories/2022/03/collaboration-good-fit-wearable-sensor-startup
58. Dezeen, MIT 4D-knit dress with Ministry of Supply: https://www.dezeen.com/2024/02/09/4d-knit-dress-mit-ministry-of-supply/
59. Mintz, Massachusetts bet on AI and robotics: https://www.mintz.com/insights-center/viewpoints/2236/2026-07-15-massachusetts-making-major-bet-ai-and-robotics-your
60. Boston Globe, Massachusetts robotics and AI startups: https://www.bostonglobe.com/2026/09/24/business/mass-robotics-ai-startups/
61. MassTech, robotics: https://masstech.org/robotics
62. Hacker News comment on an apparel exoskeleton collaboration: https://news.ycombinator.com/item?id=50020741
