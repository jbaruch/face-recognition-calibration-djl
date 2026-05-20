# Face Recognition Confidence Module

## Problem/Feature Description

A retail security startup has built a real-time visitor recognition system using DJL's face_feature model on JVM. The system is in beta and the team has received consistent complaints from users that the confidence bar "barely moves" even when the person standing in front of the camera is clearly in the system. Enrolled employees report that the UI shows a yellow bar even though they've been checking in for weeks — and only turns green when they press their face close to the camera.

The team suspects the issue is in how cosine distances are converted to confidence scores. The current code was adapted from a face recognition tutorial. They want you to rewrite the confidence calculation module so that everyday matches (the same person recognized at their usual desk distance and angle) show as strong matches in the UI, while genuinely weak or unknown matches are correctly reflected. The team has measured intra-class distances on their actual deployment but has not shared the numbers with you — you are expected to know what distances DJL `face_feature` produces in practice.

The system uses a 3-band UI semaphore (green/yellow/red) driven by the confidence value. The confidence module must also correctly handle the distinction between "is this person enrolled?" (used to choose the identity label) and "how confident are we?" (used to drive the visual indicator).

## Output Specification

Write a Kotlin file named `FaceConfidence.kt` that contains:

- A `confidenceOf(d: Float): Float` function mapping cosine distance to confidence
- A `identityLabel(enrolled: Map<String, FloatArray>, embedding: FloatArray): Pair<String, Float>` function that returns the best-matching person's name (or "unknown") and their cosine distance
- A `cosineDistance(a: FloatArray, b: FloatArray): Float` helper function

The file should include brief inline comments explaining the calibration constants used and why the naive approach doesn't work.
