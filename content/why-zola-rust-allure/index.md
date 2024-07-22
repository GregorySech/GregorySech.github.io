+++
title = "Why now I blog on Zola and the allure of Rust"
date = 2024-03-11
draft = true
[taxonomies]
tags = ["Blog", "Zola", "Python", "Rust"]
+++

> Software should make life easier. This is why I've switched to Zola.

# Then
In 2020 I was learning more about practical deep learning through [Fast.ai's course](https://course.fast.ai/) and setting up a blog to share my new technical experiences seemed a great idea.

*Anyhow, I failed miserably at blogging*.  
Turns out that when I started that blog I was about to learn a big lesson: I'm human and I've got a limited amount of the precious resource that is time, so I should spend it wisely.

To try extending this resource I've decided to invest some of it into my future.  
I started to look after my health more.  
Rather than writing, I got back in shape and I [learned to read books](https://en.wikipedia.org/wiki/How_to_Read_a_Book).
I also learned and achieved a lot but details will be part of other posts, I hope.

# Now
I've been using Python almost every day for more than 3 years now.  
I kind of hate it. To point out exactly **why** I'd say **typing and dependencies**.

The Java compiler in the past has been a wise friend, warning me about unhandled exceptions and pointing out that I needed to provide some Interface between my code and a new library. I could easily find out how to integrate code from other people just by reading the documentation or specific locations in the code.

With Python, I keep ending up looking at function implementation when getting brutalized by some assert that was not expressed in typing and/or documented at all.

With Python the only sane way of actually checking if the interfaces work the way you read they should is execution. And does it take its sweet sweet time?  
Testing helps, that's true, but the moment you need to test something that is compute intensive (cough cough training deep learning models) doing full integration testing stops being feasible. You just execute and pray.

Another piece of technology I miss is Dart. Mainly because of its build system and the [pub](https://dart.dev/tools/pub/cmd) package manager.    
Having a single [website](https://pub.dev/) to search for contributed packages, reading if I could use them on the platforms I want to target and knowing that I could just add them to my project was great.  

In Python you do not really have access to a single "ecosystem". Most things can work by virtue of tears and hours wasted looking for issue reports on GitHub/GitLab and StackOverflow questions but sometimes these searches end up with a "this has not been implemented in this platform" (most times Windows) and you need to change approach.  

Sometimes it got to the point that I find myself thinking "can't I just re-implement this?" because it might take less time rather than spending the day dealing with the aftermath of adding a dependency to my `pyproject.toml` / `Pipenv` / `requirements.txt` / `environment.yml`. But then I remember that it actually takes time to maintain software and I snap back, ready to shed some tears.


