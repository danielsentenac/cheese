# Cheese IPU6 Branch Note

This branch contains a small GStreamer device-discovery compatibility fix for
systems that rely on modern camera providers such as `libcamera`.

- Branch: `ipu6-device-provider-filter`
- Main patch: `libcheese/cheese-camera-device-monitor.c`

## What changes

Cheese currently adds a `GstDeviceMonitor` filter only for
`"Video/Source"`. Current GStreamer source elements and modern providers use
the `"Source/Video"` class ordering.

This branch accepts both class strings so Cheese can discover those providers
instead of immediately falling back to raw `/dev/video*` nodes.

## Why this branch exists

Tested on:

- Fedora 43
- Cheese 44.1
- Intel Meteor Lake IPU6 laptop

On that system, native Cheese falls back to `/dev/video0` and fails on the raw
V4L2 path, while `libcamera` can enumerate the internal camera separately. This
patch addresses one plausible Cheese-side discovery problem, but it is probably
not sufficient by itself for complete IPU6 support.

## Status

The upstream Cheese project is archived, so this branch should be treated as a
shareable fix candidate or downstream patch rather than a guaranteed upstream
merge.
