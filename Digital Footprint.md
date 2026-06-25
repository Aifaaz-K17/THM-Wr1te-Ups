# TryHackMe - Digital Footprint | Hint-Based Write-Up

Difficulty: Easy | Category: OSINT

Room link: https://tryhackme.com/room/osintchallengeiv

This is as always, only for times when you are actually stuck, and is not in any way a replacement for your own work. OSINT Rooms in particular require persistence and investigation. Please put in the effort before resorting to hints.

---

What's This Room About?

You are asked to explore the digital presence of ACME Jet Solutions. Information about one of their employees has been leaked; this involves an image, a company website that is no longer active, a photograph of a monument and its surroundings, and a leaked internal document. Each of these has information to give, helping you learn more about the company and its employees.

This room can be described as a storytelling OSINT challenge; it involves more context than a straightforward "find the flag" type of room. It's built up in such a way that one step leads to the next and you will be using a mix of image metadata analysis, web archive exploration, reverse image searches and document forensics - all within a single, relatively short room. Given that this room is rated "easy," that's an excellent variety!

Before we get into the individual tasks, please be aware of one general rule: carefully read each task's description. Some tasks have pitfalls because students overlook critical details in the descriptions that would have steered them in the right direction, not because they were lacking any skills. When you get to one of these tasks, you will recognize it!

---

Task 1: The Leaked Photo

In the first task, you are given an image of a house and need to discover its location.

Your first attempt may be to perform a reverse image search on the photograph. That's a sensible approach in general but this image is not indexed online by search engines so you won't get anywhere. Instead, concentrate on what is embedded within the photograph, as opposed to the photo as a whole.

Photographs taken with a smartphone or even some digital cameras can include much more than simply colored pixels. When photos contain this kind of data, a tool can be used to extract it, a tool if you have prior experience with image forensics will be familiar to you.

> Need assistance? Search for "EXIF data and tools to extract". One of the most commonly utilized ones is a command-line application included with almost all versions of Linux.

Once you pull the photo's information, you will findGPS coordinates. Enter these coordinates into Google Maps and see what you come up with. If what appears doesn't seem right; maybe you end up in the middle of an empty field; double check the hemisphere. Geographic coordinates include directionality, and direction matters.

---

Task 2: The Company Website

For Task 2, you are given the domain name of the company's website, but it doesn't appear to be functioning any more. Your goal is to determine the year that the company was founded.

The absence of an active website doesn't necessarily mean there's nothing to see. The internet remembers many of its contents long after their original publication date, thanks to a network of tools designed to allow access to previous versions of websites. This is a great opportunity to learn how to use one of them if you haven't had the chance yet.

> At a standstill? Consider methods for web page archiving. There's a popular public site that's been gathering and preserving content from websites for years. Type "web archive" in your search engine, and you'll find it quickly.

After navigating to the web archiving tool, make sure to explore more than just the newest cached page. Delve into some of the archived versions, as the founding date can be found somewhere within them. It is more fruitful to carefully study the information than to skim through it rapidly.

---

Task 3: The Landmark

In Task 3, you are provided with a photo of a notable landmark, and you need to identify a building to its immediate right. I deliberately emphasized the word "right" because many people spend a lot of time on this particular task, searching for the wrong building. The prompt clearly specifies the direction to look and even gives you a significant clue about the kind of structure you should be looking for. Read this task description at least twice.

Begin your search with a reverse image search for the landmark in the photograph; the monument depicted is sufficiently famous for this to yield immediate results. Once you've confirmed its identity and location, open Google Maps and start to investigate the area around it on Street View.

Your mission is to find a building with an exterior sign on its surface. This sign might not be in your language, but that's alright, as the task is to translate the information.

> In a bind? Think about cities known for movements for independence and look for famous landmarks associated with this kind of history. The landmark in this picture is unique and gets a lot of pictures taken of it.

---

Task 4: The Leaked Document

Finally, for the last task, you have an internal document that was mistakenly published online by one of the company's developers. Your objective is to find out who was responsible for maintaining the company's systems, then to locate this person on the internet.

Your first step should be to examine the document itself, just as you would analyze the photograph in the first task. Documents often contain invisible metadata such as author fields, last-modified fields, custom properties, or even personally identifiable information that were not intended to be shared with the public.

> Difficulty reading the file? If the file opens up with nothing obvious appearing in it, consider that office file formats are archives at heart. Simply changing the file extension can enable you to peek inside the contents directly, or you can utilize a dedicated metadata viewing program.

Once you identify a username, you must now search the web for that person's presence. Fortunately, there are tools that specialize in doing exactly this: they let you check an unknown username across countless different platforms. Give one of these a try.

Not all results will point to someone actually contributing content; just because an account exists doesn't mean it's the person you're looking for. Examine your search results methodically and avoid clicking the very first link you encounter.

The last flag will be somewhere in the individual's online presence. When you find it, you'll know.

---

What's the Point of This Room?

Digital Footprint perfectly illustrates the amount of personal information that people share, often unwittingly. A simple snapshot from a smartphone may contain precise GPS coordinates of where it was snapped. A Word document will have an author's username embedded in its properties. 

Websites we assume have vanished entirely are faithfully archived for posterity. 

Usernames you might have used at one time can lead you right to other accounts you currently maintain.

The processes you employ in this room don't involve any illegal activities or traditional hacking. It all consists of things readily available to anybody that knows where to look - public information. This highlights why OSINT (Open Source Intelligence) is important from a privacy standpoint, as the very same methods that a detective would use to locate a target could also be applied to expose anyone.

If you enjoyed this room, you can easily sink much deeper down the rabbit hole. There is a robust methodology underlying OSINT, which includes identifying pivots points, corroborating information from multiple sources, and strategically deciding when to cast your net wide versus when to go in deep. The TryHackMe learning paths provide even more rooms that cover the topic in depth.

---

# Special thanks! Please take your time with task #3 and don't forget to read your descriptions!
