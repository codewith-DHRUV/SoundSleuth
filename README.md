Description 🎼
SoundSleuth is an implementation of Shazam's song recognition algorithm based on insights from these resources. It integrates Spotify and YouTube APIs to find and download songs.

Installation 🖥️
Prerequisites
Golang: Install Golang
FFmpeg: Install FFmpeg
NPM: To run the client (frontend).
Steps
Clone the repository:

git clone https://github.com/cgzirim/seek-tune.git
Install dependencies for the backend

cd seek-tune
go get ./...
Install dependencies for the client

cd seek-tune/client
npm install
Usage 🚴
▸ Start the Client App 🏃‍♀️‍➡️
# Assuming you're in the client directory:

npm start
▸ Start the Backend App 🏃‍♀️
In a separate terminal window:

cd seek-tune
go run *.go serve [-proto <http|https> (default: http)] [-port <port number> (default: 5000)]
▸ Download a Song 📥
Note: A link from Spotify's mobile app won't work. You can copy the link from either the desktop or web app.

go run *.go download <https://open.spotify.com/.../...>
▸ Save local songs to DB (supports all audio formats) 🗃️
go run *.go save [-f|--force] <path_to_song_file_or_dir_of_songs>
The -f or --force flag allows saving the song even if a YouTube ID is not found. Note that the frontend will not display matches without a YouTube ID.

▸ Find matches for a song/recording 🔎
go run *.go find <path-to-wav-file>
▸ Delete fingerprints and songs 🗑️
go run *.go erase
Example 📽️
Download a song

$ go run *.go download https://open.spotify.com/track/4pqwGuGu34g8KtfN8LDGZm?si=b3180b3d61084018
Getting track info...
Now, downloading track...
Fingerprints saved in MongoDB successfully
'Voilà' by 'André Rieu' was downloaded
Total tracks downloaded: 1
Find matches of a song

$ go run *.go find songs/Voilà\ -\ André\ Rieu.wav
Top 20 matches:
        - Voilà by André Rieu, score: 5390686.00
        - I Am a Child of God by One Voice Children's Choir, score: 2539.00
        - I Have A Dream by ABBA, score: 2428.00
        - SOS by ABBA, score: 2327.00
        - Sweet Dreams (Are Made of This) - Remastered by Eurythmics, score: 2213.00
        - The Winner Takes It All by ABBA, score: 2094.00
        - Sleigh Ride by One Voice Children's Choir, score: 2091.00
        - Believe by Cher, score: 2089.00
        - Knowing Me, Knowing You by ABBA, score: 1958.00
        - Gimme! Gimme! Gimme! (A Man After Midnight) by ABBA, score: 1941.00
        - Take A Chance On Me by ABBA, score: 1932.00
        - Don't Stop Me Now - Remastered 2011 by Queen, score: 1892.00
        - I Do, I Do, I Do, I Do, I Do by ABBA, score: 1853.00
        - Everywhere - 2017 Remaster by Fleetwood Mac, score: 1779.00
        - You Will Be Found by One Voice Children's Choir, score: 1664.00
        - J'Imagine by One Voice Children's Choir, score: 1658.00
        - When You Believe by One Voice Children's Choir, score: 1629.00
        - When Love Was Born by One Voice Children's Choir, score: 1484.00
        - Don't Stop Believin' (2022 Remaster) by Journey, score: 1465.00
        - Lay All Your Love On Me by ABBA, score: 1436.00

Search took: 856.386557ms

Final prediction: Voilà by André Rieu , score: 5390686.00
Database Options 👯‍♀️
This application uses SQLite as the default database, but you can switch to MongoDB if preferred.

Using MongoDB
Install MongoDB

Configure MongoDB Connection:
To connect to your MongoDB instance, set the following environment variables:

DB_TYPE: Set this to "mongo" to indicate using MongoDB.
DB_USER: The username for your MongoDB database.
DB_PASS: The password for your MongoDB database.
DB_NAME: The name of the MongoDB database you want to use.
DB_HOST: The hostname or IP address of your MongoDB server.
DB_PORT: The port number on which your MongoDB server is listening.
Note: The database connection URI is constructed using the environment variables.
If the DB_USER or DB_PASS environment variables are not set, it defaults to connecting to mongodb://localhost:27017.

