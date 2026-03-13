# Procedural Creature Engine -- AI Agent Implementation Specification

## 1. Project Objective

Build a browser-based procedural creature generation engine.

Pipeline:

DNA → Skeleton Graph → Mesh → Skin/Texture → Animation → Rendering →
Evolution

The system must: - Automatically generate unique creatures - Use a
joint-based skeletal structure - Support mutation and crossover - Render
in HTML Canvas or WebGL - Allow large-scale procedural variation

------------------------------------------------------------------------

# 2. System Architecture

Modules:

core/ math/ dna/ skeleton/ generator/ mesh/ rendering/ animation/
simulation/

Total expected size: 2000--5000 lines.

------------------------------------------------------------------------

# 3. File Structure

creature-engine/ │ ├── index.html ├── main.js │ ├── core/ │ ├──
engine.js │ └── config.js │ ├── math/ │ ├── vector.js │ ├── matrix.js │
└── noise.js │ ├── dna/ │ ├── dna.js │ ├── mutation.js │ └──
crossover.js │ ├── skeleton/ │ ├── skeleton.js │ ├── joint.js │ └──
bone.js │ ├── generator/ │ ├── creatureGenerator.js │ ├──
limbGenerator.js │ └── bodyGenerator.js │ ├── mesh/ │ ├── meshBuilder.js
│ └── skinBuilder.js │ ├── rendering/ │ ├── renderer.js │ ├──
lighting.js │ └── shading.js │ ├── animation/ │ ├── animator.js │ └──
gaitGenerator.js │ └── simulation/ ├── physics.js └── evolution.js

------------------------------------------------------------------------

# 4. DNA System

DNA defines creature parameters.

Example genes:

bodySize bodySegments limbCount limbLength limbSegments symmetry
eyeCount tailLength skinHue skinPattern

Functions:

random() mutate() crossover() serialize() deserialize()

Example:

DNA.random() DNA.mutate() DNA.crossover(parentA,parentB)

------------------------------------------------------------------------

# 5. Skeleton System

Entities:

Joint - position - rotation - parent - children

Bone - startJoint - endJoint - thickness

Skeleton - root - joints\[\] - bones\[\]

Example hierarchy:

      head
       |
     torso

/ \|\
arm leg leg

------------------------------------------------------------------------

# 6. Creature Generator

Input: DNA Output: Skeleton graph

Steps:

1.  Generate torso
2.  Attach limbs
3.  Generate joint chains
4.  Build skeleton graph

Pseudo:

for limb in dna.limbCount: chain = createJointChain() attach(chain,
torso)

------------------------------------------------------------------------

# 7. Mesh Builder

Purpose: Convert skeleton to renderable body.

Algorithm:

bone → capsule shape → polygon mesh

Each bone becomes a cylinder/capsule.

Steps:

1.  Iterate bones
2.  Build mesh segments
3.  Merge mesh
4.  Apply smoothing

------------------------------------------------------------------------

# 8. Skin / Texture

Procedural texture generation.

Methods:

Perlin Noise Simplex Noise Voronoi Pattern

Outputs:

spots stripes alien skin

------------------------------------------------------------------------

# 9. Animation System

Joint constraints.

Example motion:

angle = sin(time)

Supported gaits:

walk crawl swim

Algorithm:

for joint: apply periodic rotation

------------------------------------------------------------------------

# 10. Renderer

Rendering pipeline:

clear canvas draw mesh apply shading draw details

Support:

HTML Canvas WebGL

------------------------------------------------------------------------

# 11. Evolution System

Genetic algorithm.

population selection mutation crossover

Steps:

generate population evaluate fitness select parents breed next
generation

------------------------------------------------------------------------

# 12. Development Roadmap

Phase 1 -- Core Engine Vector math Canvas renderer

Phase 2 -- Skeleton generator DNA Joint chains

Phase 3 -- Mesh system Capsule body mesh

Phase 4 -- Texture Noise patterns

Phase 5 -- Animation Walking motion

Phase 6 -- Evolution Population simulation

------------------------------------------------------------------------

# 13. Expected Code Size

Core engine 500 Generator 800 Mesh system 1000 Texture 800 Animation 600
Evolution 800

Total ≈ 4500 lines

------------------------------------------------------------------------

# End of Specification
