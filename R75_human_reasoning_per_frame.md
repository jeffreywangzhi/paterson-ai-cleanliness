# Human Reasoning: KAB Labels for R-75 Route (39 frames)

**Labeler:** Guangyuan Yang
**Date:** April 23, 2026
**Purpose:** Ground truth for AI calibration. Each frame has (1) the labeler's direct observation in natural language, (2) KAB score derived from that observation, (3) the KAB rule applied to derive the score.

**Scoring convention:**
- All 5 KAB indices (Litter / Graffiti / Vehicles / Storage / Signs) on a 1-4 scale per official KAB definitions
- Dumping is binary (T/F)
- Uncertain (Y/N) flags frames where resolution prevents a confident call
- `facility` flag marks garbage collection infrastructure that should be excluded from residential enforcement

---

## Clean baseline frames (all indices = 1, no notes needed)

The following 23 frames were judged clearly clean. All five KAB indices scored 1. The labeler's observations confirmed: residential or park settings, identifiable snow (not litter), legally parked cars, normal municipal fixtures (hydrants, utility poles, mailboxes), and no out-of-place items.

**Frames:** 0001, 0002, 0003, 0004, 0005, 0006, 0007, 0008, 0011, 0013, 0015, 0016, 0018, 0019, 0020, 0021, 0025, 0026, 0027, 0028, 0029, 0035, 0040, 0043, 0044, 0045, 0046

Representative observations:
- **0001-0002 (park):** "Park drive, snow-covered lawns, trees, benches. Street is clean."
- **0005 (residential main road):** "Snow on left lawn fully covered, right lawn shows melting snow as small white dots — clearly identifiable as snow because it is very white."
- **0018 (extremely blurry frame):** "Extremely pixelated. Melting snow appears mosaic-shaped, easily mistakable for litter. But on careful inspection, it is snow. Road is clean."
- **0024 (residential with full trash bin):** "Right side has a green trash bin full of trash. But trash bins at curb with trash in them are normal on collection day. Ground is clean." *Note: KAB baseline explicitly excludes curbside trash bins from violations. This frame is a critical test case — an AI that flags this would be producing false positives on normal city operations.*
- **0025 (oil stain):** "20-30cm black spots on road are wet — oil or water leak stain, not litter."
- **0041 (dried liquid residue):** "Right side has a large silver-gray dried liquid stain and 3 long narrow strips that could be snow or litter. I cannot determine. A dried stain is not litter." *Labeled L=1 because the dried stain is clearly not litter, and the 3 strips are indeterminate (likely snow based on context).*
- **0046 (facility entrance, no litter):** "Facility entrance. Large wet pavement with tire tracks from trucks entering/leaving. Looks dirty but I see no actual litter." *Labeled L=1 because wet pavement and tire marks are not litter. This is a good example where "visually dirty" ≠ "KAB litter violation."*

---

## Frames requiring detailed reasoning (7 frames)

### Frame 0012 — Uncertain storage / curbside cluster

**Direct observation:**
> "Main road, residential. On the left side near the camera, in front of a parked car, there is something I cannot clearly identify. It looks like a trash bin that is overflowing, with something large attached or next to it. I don't know if it's snow. On top appears to be a black trash bag, and below is a dark green bin-shaped object roughly the width of the bag. Could be illegal dumping, could be a full bin with snow on it."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 1 | No scattered small litter visible on street or sidewalk. |
| Graffiti | 1 | No graffiti. |
| Vehicles | 1 | Legally parked cars only. |
| **Storage** | **2** | One cluster of out-of-place items identified (black bag on top of green bin-shaped object). KAB level 2 = 1-4 specific out-of-place items. Cannot confirm if it is a legitimate trash bin with overflow (not a violation) or illegal dumping of bags. **Labeled 2 with uncertain=true.** |
| Signs | 1 | No signs. |
| Dumping | F | Cannot confirm dumping without clearer identification. |
| Uncertain | Y | Cannot distinguish bin-with-overflow (legal) from illegal bag drop. |

---

### Frame 0017 — Two cylindrical objects, not municipal fixtures

**Direct observation:**
> "Main road with houses, trees, guardrails, lawn, and snow both regular and irregular on both sides. On the left of the camera, there are two gray, dark gray cylindrical objects. They are stuck together, looking like one unit, clustered against the background. They are NOT a mailbox or a hydrant. About one meter tall, roughly the height of a car's front hood, maybe slightly shorter. It is NOT illegal dumping of trash — it is storage / clutter. Below them is an irregular wide strip of snow."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 1 | No scattered small litter. |
| Graffiti | 1 | No graffiti. |
| Vehicles | 1 | Legally parked. |
| **Storage** | **2** | Two cylindrical out-of-place objects (not hydrants, not mailboxes, not trash bins). Approximately 1m tall. KAB level 2 = 1-4 specific identifiable out-of-place items. Score = 2. |
| Signs | 1 | No signs. |
| Dumping | F | Not bulk items (furniture/mattress/appliances). |
| Uncertain | N | Confident these objects are out-of-place; uncertain only about what they exactly are, not whether they are out-of-place. |

---

### Frame 0022 — Clear scattered litter (the strongest positive case)

**Direct observation:**
> "Main road with residential houses both sides. The right side has mosaic-shaped scattered snow, identifiable as snow. On the **left side**, there is a wide white house with a narrow lawn in front. The lawn is partially bordered by a green fence, and outside the fence is the sidewalk, then another thin lawn strip, then the parking lane. From the fence all the way to the left edge of the frame — **across the first lawn, the sidewalk, the second lawn strip, and the parking lane — there is scattered small litter throughout**. Mixed with snow, but clearly identifiable as litter because the distribution is dense. The area is about 4-5 meters long and 3 meters wide. All fragments of small litter."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| **Litter** | **3** | Scattered litter dominates a 4-5m × 3m zone. Distribution catches the eye repeatedly. KAB level 3 = "dozens of items, litter catches eye repeatedly, gutters with accumulated trash." Not level 4 because no piled trash bags or overwhelming accumulation — just widely scattered small fragments. |
| Graffiti | 1 | No graffiti mentioned. |
| Vehicles | 1 | Legally parked. |
| Storage | 1 | No out-of-place large items. |
| Signs | 1 | No signs. |
| Dumping | F | No bulk items (no furniture, mattress, appliances). |
| Uncertain | N | Confident identification of scattered litter in bounded zone. |

**Comment for calibration:** This is the "gold standard" positive test case. If the AI produces a high litter score here (3 or 4), the system is working at peak capability. If the AI misses this or scores only 1-2, it would indicate a systematic miss on a clear case.

---

### Frame 0023 — Genuinely unresolvable (resolution limit case)

**Direct observation:**
> "Main road, but the blocks adjacent are not residential — they are two large buildings, each about one block wide. Cars parked both sides. Left edge of frame has scattered mosaic-shaped objects. I genuinely cannot determine if this is snow or litter. Because this frame is adjacent to frame 0022 in location, it could be spillover of real litter, OR it could be identical snow patches to the dozens of other snowy frames on this route. I cannot distinguish at this resolution."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 1 | Defaulting to conservative score per KAB small-item rule: "when in doubt about small items, score 1." |
| Graffiti | 1 | None mentioned. |
| Vehicles | 1 | Legal parking. |
| Storage | 1 | None. |
| Signs | 1 | None. |
| Dumping | F | None. |
| **Uncertain** | **Y** | **Human labeler cannot resolve snow vs litter at this resolution.** This frame is a direct test of the resolution limitation we document in the calibration report. |

---

### Frame 0034 — Uncertain bin cluster with snow coating

**Direct observation:**
> "Main road, houses both sides. Left side at frame edge, there appears to be 1 or 2 green trash bins. Underneath them, there is a thick black object that is mostly white (snow-covered) but shows black underneath in a few spots. The item has a top layer of melting snow but the black underneath looks like it has depth — it could be snow on top of ground, OR snow on top of dumped material. Could be just snowy ground next to a bin, could be illegal dumping coated in snow. Next to or attached to the bin. The bin lid looks pink or purple in the lighting."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 1 | No scattered small litter in road. |
| Graffiti | 1 | None. |
| Vehicles | 1 | Legal parking. |
| **Storage** | **2** | Conservative score = 2 based on "black object with depth beneath snow coating, attached to bin cluster." Could be snow-covered ground (storage=1) or snow-covered dumped items (storage=2-3). Labeling 2 with uncertain=true. |
| Signs | 1 | None. |
| Dumping | F | Cannot confirm without seeing what is under the snow. |
| Uncertain | Y | Snow coating prevents identification of what is underneath. |

---

### Frame 0036 — Snow patch in road center (classic common-sense case)

**Direct observation:**
> "Road with houses both sides. Right side sidewalk has scattered snow patches. In the **middle of the road itself**, there is a small white patch about the length and width of a car tire. Honestly I cannot see clearly if it is snow or litter. Using common sense I can tell it is probably snow that hasn't melted because the car wheels haven't rolled over that spot. But AI cannot reason with common sense about car wheel tracks."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 1 | Conservative score. Common-sense reasoning says snow. |
| All other | 1 | Clean scene otherwise. |
| Dumping | F | No. |
| **Uncertain** | **Y** | **Labeled uncertain specifically to document the "common-sense gap" — humans use contextual reasoning (wheel tracks imply snow) that AI does not have access to.** |

**Comment for calibration:** This frame is valuable as a documentation piece. It shows the type of reasoning humans use that current vision models cannot replicate, supporting the "higher resolution cameras would help, but so would context" argument.

---

### Frame 0042 — Small cardboard box behind parked car

**Direct observation:**
> "Garbage truck left-turning at intersection. Facing the truck's future lane. In front of the truck there is a fenced parking lot. Below the fence is a narrow lawn strip curving around the corner. **On that lawn, under the right wheel of a parked white car, there is a brown cardboard box.** It is out of place. But — it is smaller than the wheel height. And it is right next to three fence posts. Even a human has to look carefully to see it. AI may miss it entirely."

**KAB scoring:**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 1 | Single cardboard box is a single item, small, partially hidden. Conservative score. |
| All other | 1 | Otherwise clean. |
| Dumping | F | Single small cardboard box is not bulk item dumping. |
| **Uncertain** | **Y** | **Labeled uncertain because the item is at the detection threshold — this is expected to be a likely AI miss and a useful data point for documenting the small-item detection floor.** |

**Comment for calibration:** This frame tests the lower bound of detection. Missing this frame is not a failure of the prompt — it is a genuine resolution/visibility limit.

---

## Facility frames (excluded from residential enforcement, labeled for completeness)

### Frame 0047 — Garbage facility interior

**Direct observation:**
> "This is the garbage facility's interior. Muddy, pitted ground with water in the pits. In front of the truck there are piles of construction-like materials — steel bars or wood, thick rods — I can't tell exactly what. There is another large clutter of unidentified items, roughly 1m × 1m × 1m, obviously not normal items. Garbage trucks, large containers. The whole area looks very dirty."

**KAB scoring (what AI should score if blind to context):**
| Index | Score | Rule applied |
|-------|-------|-------|
| Litter | 3 | Debris scattered across muddy lot. |
| Storage | 4 | Massive accumulation of material, consistent with KAB level 4. |
| Dumping | T | Construction-like materials visible. |
| **Facility flag** | **TRUE** | **This is a city-operated garbage collection facility. AI detection is technically correct, but no enforcement should be triggered. Production system needs a facility exclusion list from Bandana.** |

### Frame 0048 — Garbage truck depot

**Direct observation:**
> "Garbage truck depot. A small gray 3-meter-long structure like a guard booth. To its left, hollow concrete blocks are stacked with snow on top, and there is a barrel next to them. Looks disorganized."

**KAB scoring (what AI should score if blind to context):**
| Index | Score | Rule applied |
|-------|-------|-------|
| Storage | 3 | Pile of concrete blocks and barrel. KAB level 3 = pile that would fill a small shed. |
| **Facility flag** | **TRUE** | **Same as 0047. Depot location. Excluded from residential enforcement.** |

---

## Missing frames (video segments where truck was stationary or GPS speed filter removed)

**Frames not present:** 0009, 0010, 0030, 0031, 0032, 0033, 0037, 0038, 0039

Total: 9 missing out of 48-frame potential sequence = 39 analyzed frames.

---

## Summary statistics for calibration

| Category | Count |
|----------|------:|
| Total frames analyzed | 39 |
| Missing frames | 9 |
| Decidable frames (labeler can commit to a score) | 30 |
| Frames where labeler is uncertain | 5 (0012, 0023, 0034, 0036, 0042) |
| Frames scored all-1 (clean) | 23 |
| Frames with at least one score ≥ 2 (non-facility) | 5 (0012, 0017, 0022, 0034 [all storage=2], 0022 [litter=3]) |
| Facility frames (excluded from residential enforcement) | 2 (0047, 0048) |
| Frames with dumping=T | 1 (0047, facility only) |
| Frames with clear single dominant issue | 1 (0022 = strong litter) |

**Interpretation for calibration:**
- The labeled dataset contains very few strong positive examples for bulk item detection. R-75 was a residential sweep in winter; Bandana's newer footage (with couches, mattresses) should be the ground truth for bulk item calibration, not this dataset.
- The labeled dataset is strong for **distinguishing snow from litter at 640×360** — this is the dominant challenge and the labeled uncertainties (5 frames) directly quantify the resolution limit.
- Frame 0022 is the only strong clear-positive (litter=3). Frame 0017 is the only clear outside-storage positive in a residential context. Frames 0012 and 0034 are uncertain storage/dumping cases that a human-in-the-loop review layer would correctly flag for human attention.
