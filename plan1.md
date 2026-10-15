This plan works for both CATIA V5 and 3DEXPERIENCE (CATIA V6). Choose your standard once at the start - it drives everything else.

### 1. Project Inputs - What I Need From You

Before we start, freeze these 3 decisions:

| Input | Options | Recommendation |
| :--- | :--- | :--- |
| **Standard** | ISO 1101 / ISO 8015 / GPS vs. ASME Y14.5-2018 | **ISO GPS** for Europe/Middle East, **ASME** for North America |
| **Source Data** | CATPart (single part) or CATProduct (assembly) | Determines if we do Part Drawing or Assembly Drawing + BOM |
| **Drawing Purpose** | Manufacturing + Inspection, or MBD/FTA 3D Master | Defines tolerance density and view count |
| **General Tolerance** | e.g. ISO 2768-mK, ISO 2768-fH, or custom block | Must be in title block if not toleranced explicitly |

> **Please confirm: 1) Your standard (ISO or ASME)? 2) Part or Product? 3) Do you have a company title block template (.CATDrawing)?**

### 2. The 6-Phase Project Plan

#### PHASE 0: Preparation (1-2 hours)
1.  Analyze 3D: Identify Functional Surfaces (mating, sealing, guiding), Manufacturing process (machined, sheet metal, cast, plastic), and Critical characteristics
2.  Define Datum System: Select Primary-Secondary-Tertiary datums based on assembly function (e.g. Datum A = mounting face, Datum B/C = locating holes)
3.  Prepare Template: Set up `A2/A3` sheet, projection method (First Angle / Third Angle), scale, title block, layer filters, and Generative View Style
4.  Clean 3D: Check part has no open bodies, all fillets/chamfers are features, not dress-ups

#### PHASE 1: View Generation - Generative Drafting Workbench
You don't draw views, you generate them from 3D.

*   **Main Views:** `Front View` + `Unfolded/Projection Views` (Top, Left/Right)
*   **Derived Views:** `Offset Section View / Section Cut`, `Aligned Section View` (for angled features), `Detail View` (for small features, scale 2:1 / 5:1), `Auxiliary View` (for inclined planes)
*   **3D View:** `Isometric View` with shaded mode for readability
*   **For CATProduct:** Add `Exploded View` (Isometric), `Bill of Material (BOM)` + `Balloons`, `Assembly Section` and `Overload Properties`

> CATIA Command: `Start > Mechanical Design > Drafting > New Sheet > Front View > Select reference plane from 3D`

#### PHASE 2: Meaningful Dimension System
This is not auto-dimensioning. Every dimension must have a purpose: **Function > Manufacturing > Inspection**.

*   **Functional Dimensions:** Dimensions that control assembly (hole distances, mating lengths)
*   **Non-Functional:** Auxiliary dimensions in brackets `( )` for reference only
*   **Strategy:**
    1.  External block dimensions (Overall Length/Width/Height)
    2.  Internal functional dimensions (Hole patterns, slots, steps)
    3.  Detail dimensions (Fillets R, Chamfers C, Thread M, Counterbore)
*   **CATIA Tools:** `Dimensions > Chained / Cumulative / Stacked`, `Thread Dimensions`, `Hole Dimension Table`, `Coordinate Dimensions`, `Fillet/Chamfer Auto-Create`

#### PHASE 3: Full Tolerance System (The Core)
This makes the drawing meaningful. 4 layers:

**A) Dimensional Tolerances (ISO 286)**
*   Linear tolerances with fit class: e.g. `25 H7/g6`, `Ø20 H7`
*   Angular tolerances: `±0°30'`
*   General tolerance block: `ISO 2768-mK` in title block

**B) Geometric Tolerances (GD&T / GPS - ISO 1101)**
*   **Form:** Flatness, Straightness, Circularity, Cylindricity
*   **Orientation:** Parallelism, Perpendicularity, Angularity (with datums)
*   **Location:** Position (for hole patterns - most important), Concentricity, Symmetry
*   **Run-out:** Circular Run-out, Total Run-out
*   **CATIA Tools:** `Tolerance > Geometrical Tolerance` palette, `Datum Feature` symbol, `Datum Target`

**C) Surface & Material Specifications**
*   Surface Roughness: `Ra 0.8`, `Ra 3.2` on functional faces
*   Edge Conditions: `ISO 13715`, Burr-free
*   Hardness / Heat Treatment / Coating notes
*   **CATIA Tools:** `Roughness Symbol`, `Welding Symbol` (if applicable)

**D) Tolerance Stack-up Validation**
*   Verify chain does not over-constrain (no closed loop of tolerated dimensions)
*   Use `CATIA FTA & Tolerance Advisor` to check consistency

#### PHASE 4: Annotations & Dress-Up
*   Center Lines, Axis, Threads (TAP/DRILL), Hatching (ANSI/ISO pattern)
*   Notes: `1. BREAK ALL SHARP EDGES 0.2x45°`, `2. SURFACE TREATMENT...`
*   Technical Requirements block
*   Revision Table

#### PHASE 5: Checking & Release
1.  **Design Checker:** Run `Tools > Standards Check` against your ISO/ASME XML
2.  **Print Check:** `File > Print` preview for line weights, font sizes (min 2.5mm text height)
3.  **3D-2D Link Check:** Test associativity - change 3D, update drawing (`Edit > Update`)
4.  Export: `CATDrawing` (master) + `PDF` (release) + `DXF/DWG` (for CAM/laser)

### 3. Complete Feature Checklist for Your Drawing

Use this as acceptance criteria:

**View Features:**
- [ ] Front / Top / Side views (correct projection)
- [ ] ≥1 Section View (through key internal features)
- [ ] 1 Detail View (if small features <5mm)
- [ ] Isometric View (3D understanding)
- [ ] BOM + Balloons (if CATProduct)

**Dimension System:**
- [ ] Overall dimensions
- [ ] Functional dimensions (all datum-related)
- [ ] Hole Pattern Table / Coordinate Table
- [ ] Thread, Chamfer, Fillet, Counterbore dimensions
- [ ] No duplicated or redundant dimensions

**Tolerance System:**
- [ ] General tolerance in Title Block (e.g. ISO 2768-mK)
- [ ] Fits on shafts/holes (H7/k6 etc.)
- [ ] Datum System (A|B|C) defined on frame
- [ ] Position tolerance on all hole patterns
- [ ] Form/Orientation tolerance on critical faces (Flatness, Perpendicularity)
- [ ] Ra roughness symbols on all machined faces
- [ ] Chamfer/Edge break tolerances

**Documentation:**
- [ ] Company Title Block filled (Material, Weight, Scale, Author, Date)
- [ ] Tolerance & Surface finish legend
- [ ] Revision block
- [ ] PDF + DXF exported

### 4. CATIA Feature Recommendation

For a **modern workflow**, I recommend this hybrid:

1.  **Create FTA in 3D first (Functional Tolerancing & Annotation workbench):** Apply GD&T directly on the 3D model. This is the 3D Master.
2.  **Generate 2D from FTA:** In Drafting, use `Generate Dimensions from 3D` + `Generate Balloons`. This guarantees 100% associativity and avoids manual errors.

If your 3D is not FTA-ready, we do classic Interactive Drafting.

**Next Step:** Send me a screenshot or the CATPart file, and tell me your **Standard (ISO/ASME)**. I will then generate the exact Datum scheme and view list for your specific geometry and give you a ready-to-use CATDrawing template.
