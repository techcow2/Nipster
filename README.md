# Nipster

<img width="400" height="212" alt="transparent_logo" src="https://github.com/user-attachments/assets/7c79fc6a-3f50-4d34-be74-3ca2b15a2fbd" />


A nostalgic Windows 95-style music discovery and download application that allows users to search for music on YouTube, convert videos to MP3 format, and manage their local music library.

## Features

- **YouTube Music Search**: Search for music using artist and title queries
- **MP3 Conversion**: Convert YouTube videos to MP3 format with various bitrate options
- **Library Management**: Organize and manage your downloaded music collection
- **Playlist Support**: Create and manage custom playlists
- **Cross-Platform**: Runs on Windows, macOS, and Linux


### Development

To run the application in development mode:

```bash
npm run dev
```

This will start both the Electron application and the backend server concurrently.

### Production

To build and run the application in production mode:

```bash
npm run build
npm start
```

### Building Distributables

To create distributable packages for your platform:

```bash
npm run make
```

This will create installers in the `out` directory.

Cross-platform builds can be created with:

```bash
npm run build-all
```

Platform-specific builds:
- Windows: `npm run build-win`
- macOS: `npm run build-mac`
- Linux: `npm run build-linux`

## Architecture

### Frontend

The frontend is built with React and styled with Tailwind CSS to achieve the Windows 95 aesthetic. Key components include:

- [NipsterSearchSection](src/components/NipsterSearchSection.jsx): Handles search input and parameters
- [NipsterResultsTable](src/components/NipsterResultsTable.jsx): Displays search results with download options
- [Library](src/components/Library.jsx): Manages downloaded music files
- [PlaylistManager](src/components/PlaylistManager.jsx): Handles playlist creation and management
- [Radio](src/components/Radio.jsx): Provides access to internet radio stations
- [GlobalAudioPlayer](src/components/GlobalAudioPlayer.jsx): Controls audio playback

### Backend

The backend consists of two main servers:

1. **Main Server** (port 3000): Handles API requests for search, library management, and playlist operations
2. **Conversion Server** (port 3003): Manages YouTube to MP3 conversion processes

### YouTube Integration

Nipster uses a proxy-based approach to search and convert YouTube videos:

1. Search queries are sent to the backend server
2. The server performs the YouTube search using Puppeteer
3. When a user chooses to download, the backend uses yt-dlp to convert the video
4. Converted files are stored in the `downloads` directory

## API Endpoints

### Main Server (Port 3000)

- `GET /api/search`: Search YouTube for music
- `GET /api/library`: Retrieve list of downloaded files
- `GET /api/stream/:filename`: Stream audio files
- `DELETE /api/library/:filename`: Delete a file from library
- `PUT /api/library/:filename`: Rename a file
- `POST /api/library/:filename/reveal`: Reveal file in file explorer
- `GET /api/playlists`: Retrieve all playlists
- `POST /api/playlists`: Create a new playlist
- `PUT /api/playlists/:id`: Update a playlist
- `DELETE /api/playlists/:id`: Delete a playlist

### Conversion Server (Port 3003)

- `POST /api/convert`: Convert YouTube video to MP3

## File Structure

```
nipster/
├── src/                 # React frontend components
│   ├── components/      # UI components
│   ├── contexts/        # React contexts for state management
│   ├── utils/           # Client-side utility functions
├── downloads/           # Downloaded MP3 files (created at runtime)
├── server.js            # Main server implementation
├── electron-main.js     # Electron main process
├── package.json         # Project dependencies and scripts
└── README.md            # This file
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## Disclaimer

By using this application, you agree that you will not use it to download, distribute, or otherwise acquire any copyrighted material in violation of applicable laws. You are solely responsible for ensuring that your use of this software complies with all relevant copyright and intellectual property laws.

This software is provided for educational and personal use only. The developers are not responsible for any misuse of the application.

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/techcow2/Nipster/blob/master/LICENSE) file for details.

## Acknowledgments

- Windows 95 UI inspiration
- yt-dlp for video conversion capabilities
- Electron for cross-platform desktop application support
