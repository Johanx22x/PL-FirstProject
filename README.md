# Programming Languages First Project

This is the first project of the Programming Languages course at the Instituto
Tecnológico de Costa Rica. The project consists of a server and a client that
communicate through a socket. The server is written in Go taking advantage of
the concurrency features of the language, HLS streaming protocol and the
imperative paradigm. The client is written in F# using the functional paradigm, 
Avalonia framework for the GUI and VLC for multimedia playback.

Authors:

- [Johan Rodríguez](https://github.com/Johanx22x)
- [Aaron González](https://github.com/zSnails)

## Usage

### Documentation

The documentation of the project can be found in the `doc` folder. The PDF 
document is under the name `main.pdf` in the `output` folder. This document 
is generated using LaTeX and the source code is in the `src` folder.  If the
document is not present, it can be generated by running the following command in
the `doc` folder:

```bash
make
```

### Server

The server is called `plyr` and it is located in the `server` folder, as well 
as in [zSnails/plyr](https://github.com/zSnails/plyr). The server can be compiled by
running the following command in the `server` folder:

```bash
go build
```

If the compilation fails, it is possible due to your C compiler that does not
support a 64-bit architecture. In that case, you can try to compile the server
using the `Dockefile` in the `server` folder. To do so, run the following
command in the `server` folder:

```bash
docker build . -t plyr
```

By default, the server will listen on port 8080. This can be changed by
specifying the port when running the server or docker image. To run the server,
run the following command in the `server` folder:

```bash
# If compiled
./plyr -port <port>

# If using docker
docker run -it -p <port>:8080 plyr
```

To add songs to the server, the server must be running. Then, the songs must be
added using the `add` command. The `add` command receives the song file path, 
after that, the server will ask for the song related information.

```bash
# If compiled
>>> add
File> <song file path>

# If using docker

# Copy songs to the container
docker cp <song> <the container_id>:/app/songs

# If the container is stopped, start it
docker start <the container_id>

# Attach to the container
docker attach <container_id>

# Now use add command for each song
>>> add
File> /app/songs/<song>
```

Plyr also have a TUI that can be used to interact with the server. To use the
TUI, run the following command in the `server` folder:

```bash
# If compiled
./plyr -tui

# If using docker, and the container is not created
docker run -it -p 8080:8080 plyr -tui
```

#### API Documentation

The server registers each song using a hash in the database. The hash is
generated using the song name and artist. The server exposes an API that can be
used to get the songs. The API is documented below:

```bash
# Get all songs
localhost:<port>/api/songs/

# Get song by hash/query
localhost:<port>/api/songs/<hash|query>

# Stream song by hash, using HLS protocol
localhost:<port>/<hash>/outputlist.m3u8
```

### Client 

The client is called `SharpBeat` and it is located in the `SharpBeat` folder, as
well as in [Johanx22x/SharpBeat](https://github.com/Johanx22x/SharpBeat). The client
uses the [Avalonia framework](https://github.com/fsprojects/Avalonia.FuncUI) 
for the GUI and [LibVLC](https://www.videolan.org/vlc/libvlc.html) in Windows and 
[LibVLCSharp](https://github.com/videolan/libvlcsharp) in Linux for multimedia
playback using HLS protocol. The client can be compiled by running the following
command in the `SharpBeat` folder:

```bash
dotnet build
```

To run the client, run the following command in the `SharpBeat` folder:

```bash
dotnet run
```

If you feel that the client is too slow, It is due to the fact that the client
is requesting the songs from the server. To solve this, you can run the server
before running the client. The client will try to connect to the server in the
default port (8080), this port is hardcoded in the client, so if you want to
change it, you will have to change it in the source code.

#### Client Architecture

The client has a simple architecture, each component is independent and it is
connected to the `MainWindow`. The `MainWindow` is the main component of the
client, it is responsible for rendering the UI and it is connected to the
`Backend`, `DB` and `Models` modules. The `Backend` module is responsible for
handle the communication with the server and handle the playback of the songs.
The `DB` module is responsible for handle the database, in which the playlists
are locally stored. The `Models` module is responsible for handle the data
models of the client, like the songs and play types.

The `GUI` module is where the UI is defined, there are all the UI components
that are used in the `MainWindow`. Such as the `PlayBar`, `SearchBar`, `DurationFilter`,
and others. There is a context that is used to handle the state of the UI and the 
events that are triggered by the UI. Songs and Playlists are dynamically created and 
handled during the client runtime. In the `MainWindow`, there are the 
main functions that are used to Filter/Map the songs and playlists.

This architecture can be improved by using a more functional approach, but due
to the ignorance about Avalonia and F#, it was not possible to implement it in
a more functional way in the given time. With a proper refactoring, the client
can be improved in terms of performance and code readability.

#### Client Usage

The client is pretty straightforward, it has a search bar that can be used to
search for songs, a dropdown menu that can be used to filter the songs by
genre, and a duration filter that can be used to filter the songs by duration.
It is important to note that each filter is independent, so if you filter by
genre and then by duration, only the duration filter will be applied.

The client has a Songs and Playlist tab at the left, the Songs tab shows all the
songs that match the filters or Playlists, and the Playlist tab shows all the
playlists that have been created.

On the right, there is a toolbar that can be used to refresh the songs filters in
songs tab, and in the playlist tab, it can be used to create a new playlist.

Each item in the Songs and Playlist tab has a context menu that can be used to
specific actions. It can be accessed by right-clicking the item. In the songs 
tab the context menu has the options to add or delete the song from a playlist,
and in the playlist tab, the context menu has the options to delete a playlist.

At the bottom, there is a player that can be used to play the songs. The player
has the basic controls, play, pause, next, and previous. It also has a slider
for the volume and a slider for the song progress. At the top of these controls,
there is a label that shows the current song and the song artist.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file
for details.