# API Routers

## Auth Routes
- **POST** `/auth/register` - Register User
- **POST** `/auth/login` - Login User
- **POST** `/auth/logout` - Logout User
- **GET** `/auth/me` - Get Me
- **GET** `/auth/refresh` - Refresh Token

## Users Routes
- **GET** `/users/{user_id}` - Get User
- **PUT** `/users/{user_id}` - Update Entire User
- **DELETE** `/users/{user_id}` - Delete User
- **PATCH** `/users/{user_id}` - Partly Update User
- **GET** `/users/{user_id}/friends` - Get User Friends
- **POST** `/users/{user_id}/friends/{friend_id}` - Add Friend
- **DELETE** `/users/{user_id}/friends/{friend_id}` - Delete Friend

## Films Routes
- **GET** `/films` - Get Films
- **POST** `/films` - Add Film (for Admins)
- **GET** `/films/{film_id}` - Get Film
- **PUT** `/films/{film_id}` - Edit Entire Film (for Admins)
- **DELETE** `/films/{film_id}` - Delete Film (for Admins)
- **PATCH** `/films/{film_id}` - Partly Edit Film (for Admins)

## TV Series Routes
- **GET** `/series` - Get Series
- **POST** `/series` - Add New Series (for Admins)
- **GET** `/series/{series_id}` - Get One Series
- **PUT** `/series/{series_id}` - Edit Entire Series (for Admins)
- **DELETE** `/series/{series_id}` - Delete Series (for Admins)
- **PATCH** `/series/{series_id}` - Partly Edit Series (for Admins)
- **GET** `/series/{series_id}/seasons` - Get Seasons
- **GET** `/series/{series_id}/seasons/{season_id}` - Get Season
- **GET** `/series/{series_id}/seasons/{season_id}/episodes` - Get Episodes
- **GET** `/series/{series_id}/seasons/{season_id}/episodes/{episode_id}` - Get Episode

## Chats Routes
- **GET** `/chats` - Get Chats
- **POST** `/chats` - Create Chat
- **DELETE** `/chats/{chat_id}` - Delete Chat
- **GET** `/chats/{chat_id}` - Get Chat
- **PATCH** `/chats/{chat_id}` - Partly Update Chat

## Chat Messages Routes
- **GET** `/chats/{chat_id}/messages` - Get Chat Messages
- **POST** `/chats/{chat_id}/messages` - Send Message

## Watch Parties Routes
- **GET** `/watch-parties` - Get Watch Parties
- **POST** `/watch-parties` - Create Watch Party
- **GET** `/watch-parties/{party_id}` - Get Watch Party
- **DELETE** `/watch-parties/{party_id}` - Delete Watch Party (for Owner)
- **POST** `/watch-parties/{party_id}/join` - Join Watch Party
- **DELETE** `/watch-parties/{party_id}/leave` - Leave Watch Party

## Favorites Routes
- **GET** `/favorites` - Get Favorites
- **POST** `/favorites/{content_id}` - Add To Favorites
- **DELETE** `/favorites/{content_id}` - Remove From Favorites

## Playlists Routes
- **GET** `/playlists` - Get Playlists
- **POST** `/playlists` - Create Playlist
- **PUT** `/playlists/{playlist_id}` - Update Entire Playlist
- **DELETE** `/playlists/{playlist_id}` - Delete Playlist
- **PATCH** `/playlists/{playlist_id}` - Partly Update Playlist
- **POST** `/playlists/{playlist_id}/content/{content_id}` - Remove From Playlist

## Comments Routes
- **GET** `/films/{film_id}/comments` - Get Film Comments
- **POST** `/films/{film_id}/comments` - Add Film Comment
- **DELETE** `/films/{film_id}/comments/{comment_id}` - Delete Film Comment
- **GET** `/series/{series_id}/comments` - Get Series Comments
- **POST** `/series/{series_id}/comments` - Add Series Comment
- **DELETE** `/series/{series_id}/comments/{comment_id}` - Delete Series Comment

## Rating Routes
- **GET** `/films/{film_id}/rating` - Get Film Rating
- **POST** `/films/{film_id}/rating` - Rate Film
- **GET** `/series/{series_id}/rating` - Get Series Rating
- **POST** `/series/{series_id}/rating` - Rate Series

## Streaming Routes
- **GET** `/streaming/{film_id}` - Get Stream URL
- **POST** `/streaming/{film_id}/start` - Start Stream
- **POST** `/streaming/{film_id}/pause` - Pause Stream
- **GET** `/streaming/{film_id}/status` - Get Stream Status
- **POST** `/streaming/{film_id}/seek` - Seek Stream
- **POST** `/streaming/{film_id}/save-position` - Save Stream Position
- **POST** `/streaming/{film_id}/load-position` - Load Stream Position

## History Routes
- **GET** `/history` - Get History

## Files Routes
- **POST** `/upload/film` - Upload Film
- **POST** `/upload/series/{series_id}/season/{season_id}/episode` - Upload Episode
- **POST** `/upload/cover-image` - Upload Cover Image
- **GET** `/files/{file_id}` - Get File Info
- **DELETE** `/files/{file_id}` - Delete File
