TryHackMe: Digital Footprint WalkthroughRoom Difficulty: EasyCore Concepts: Metadata Analysis, Geolocation, Archive OSINT, Document Forensics, and Username Pivoting.

Task 1: The Leaked PhotoObjective: Identify the city where the leaked company photograph was taken. Analyze the Image: We are provided with an image of a residential property and need to find its location. 
Since it's an original photo, reverse image searching won't yield reliable results. 

Extract Metadata: The easiest way to find hidden location data is to check the image's Exif (Exchangeable image file format) data. Using exiftool in the terminal:Bashexiftool <image_name>.jpg Locate Coordinates: Scroll through the output until you find the GPS Position or GPS Latitude/Longitude. You will find coordinates pointing to approximately 2612'14.8"S 2802'50.3"E. 

Geolocation: Plug these exact coordinates into Google Maps. 

Ensure you specify "South" and "East" correctly. The pin will drop in a major city in South Africa, giving you the answer for the flag. 

Task 2: Archived Company WebsiteObjective: Find the first published date of the archived company website warc-acme.com/jef/. 

The Wayback Machine: When investigating the history of a website, the Internet Archive is the gold standard. Search the Database: Instead of just using the standard Wayback Machine web interface, search the main database for the domain warc-acme.com. Analyze the WARC File: You will find an archive item (a WARC set) captured by the Archive Team. 

Find the Metadata: Look at the item's details and metadata fields. 

You are looking for a field labeled Firstfiledate. The timestamp string provided there is your flag. Task 3: Mysterious LandmarkObjective: Identify the historical building located to the right of the landmark in the provided image. Reverse Image Search: We are given an image of a tall, needle-like monument. 

Running this through Google Lens or a reverse image search quickly identifies it as the Spire of Dublin in Ireland. 

Investigate the Area: Open Google Maps and search for the Spire of Dublin.

Drop into Street View to look around the monument. Find the Building: The prompt mentions a building to the right of the landmark that played a major role in the country's fight for independence. 

Looking directly to the right of the Spire on O'Connell Street, you will see a prominent building with large pillars. The name of this building (abbreviated as the GPO) is the answer to the task. Task 4: Internal DocumentsObjective: Analyze an internal document, find a hidden username, and locate the final flag. 

Understand the File Format: We are given a document.odt file. 

OpenDocument Text (.odt) files are essentially just ZIP archives containing XML files and other formatting resources. Extract the Contents: To look under the hood, rename the extension from .odt to .zip, or simply unzip it directly in your terminal:Bashunzip document.odt Inspect the Metadata: Once extracted, you will see several files. Open the meta.xml file, which stores the document's hidden metadata (creation date, author, etc.). 

You can open it using cat, nano, or any text editor. 

Find the Breadcrumb: Inside the XML tags, you will find a user-defined field containing a username: @markwilliams7243, along with a hint regarding an upcoming "Video". The Final Pivot: Take this username and perform an OSINT search. Since the hint mentioned a video, head over to YouTube and search for the handle @markwilliams7243. 

The final flag is proudly displayed on that channel.
