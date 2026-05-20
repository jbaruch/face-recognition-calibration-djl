# Face Recognition Runtime Diagnostics and Stability

## Problem/Feature Description

A museum ticketing company has deployed a DJL-based face recognition system that lets season pass holders walk through turnstiles without scanning their card. After two months of operation, the ops team is reporting two persistent issues:

1. **Flicker**: The recognition UI flickers rapidly between "recognized" and "no face detected" as people walk through, causing inconsistent gate responses. This is particularly bad in areas with slightly uneven lighting that causes the face detector to miss frames intermittently.

2. **Ghosting and false matches**: The Haar cascade is occasionally picking up reflections and high-contrast artwork as "faces", causing spurious recognition events in the gallery area near the entrance. These false detections confuse the confidence display and occasionally trigger gate opens.

The team also wants you to add a diagnostic mode they can turn on via a system property to help them debug why certain season pass holders get rejected despite being clearly visible. The diagnostic mode should log enough information to diagnose enrollment issues vs. runtime issues.

## Output Specification

Write a Kotlin file named `RecognitionRuntime.kt` that addresses all three concerns:

- A `persistDistance` mechanism that prevents "no face" from being declared too quickly when the detector misses frames — include the appropriate hold duration as a constant
- A `isGarbageDetection(dist: Float): Boolean` function that identifies Haar false-positive faces based on their recognition distance
- A `runDiagnosticMode(enrolled: Map<String, FloatArray>, embedding: FloatArray, logger: org.slf4j.Logger)` function that logs recognition distances for all enrolled people in a format useful for debugging
- A `shouldDeclareNoFace(lastDetectionMs: Long, currentTimeMs: Long): Boolean` helper

Include comments explaining the interpretation of diagnostic output (what good vs. bad distance patterns look like).
