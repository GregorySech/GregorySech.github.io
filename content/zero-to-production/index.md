+++
title = "What I've learned from reading Zero to Production in Rust"
[taxonomies]
tags = ["Rust", "Software-Engineering", "Backend"]
draft = true
+++

# Notes
## CH 2
- Consider using a single staged CI instead of 4. Concerned about Github Action billing.
- Problem-based Learning.
  - Makes the book relevant for Rust but for different stacks too.
- User stories to capture requirements!
  - Working in iterations by starting to fulfill *most* of the requirements of all stories at first release. 
    - Then iterate to cover more and more requirements.
    - Iterate on product features, not engineering quality!

## CH 3 - The `/subscriptions` end-point.
- actix-web

- health_check to get familiar with the web framework.
  - The idea is that it's a basic/easy endpoint to start with so it will do a gradual introduction to the technology.
- Refining the requirement
  - "As a blog visitor,
     I want to subscribe to the newsletter,
     So that I can receive email updates when new content is published on the blog."
