# Data Model: Unified Streaming Application

**Feature**: Unified Streaming Application  
**Date**: 2025-01-27  
**Status**: Complete

## Entity Definitions

### IPTV Entities

#### IPTVPlaylist
Represents an IPTV playlist source with configuration and metadata.

**Fields**:
- `id: Long` - Primary key
- `name: String` - User-defined playlist name
- `url: String` - M3U/M3U8 playlist URL
- `username: String?` - Xtream Code username (nullable)
- `password: String?` - Xtream Code password (nullable)
- `serverUrl: String?` - Xtream Code server URL (nullable)
- `port: Int?` - Xtream Code port (nullable)
- `isActive: Boolean` - Whether playlist is currently active
- `lastUpdated: Long` - Timestamp of last update
- `channelCount: Int` - Number of channels in playlist

**Relationships**:
- One-to-Many with IPTVChannel
- One-to-One with EPGSource (optional)

#### IPTVChannel
Represents a single IPTV channel with streaming information and metadata.

**Fields**:
- `id: Long` - Primary key
- `playlistId: Long` - Foreign key to IPTVPlaylist
- `name: String` - Channel name
- `url: String` - Stream URL
- `logo: String?` - Channel logo URL (nullable)
- `category: String` - Channel category (Sports, News, Entertainment, etc.)
- `country: String` - Country/region identifier
- `language: String?` - Primary language (nullable)
- `quality: String?` - Quality indicator (HD, 4K, SD) (nullable)
- `isFavorite: Boolean` - Whether channel is marked as favorite
- `lastWatched: Long?` - Timestamp of last watch (nullable)
- `viewCount: Long` - View count for popularity sorting

**Relationships**:
- Many-to-One with IPTVPlaylist
- One-to-Many with EPGProgram

#### EPGSource
Represents Electronic Program Guide data source for channels.

**Fields**:
- `id: Long` - Primary key
- `playlistId: Long` - Foreign key to IPTVPlaylist
- `name: String` - EPG source name
- `url: String` - EPG XML URL
- `lastUpdated: Long` - Timestamp of last update
- `isActive: Boolean` - Whether EPG source is active

**Relationships**:
- One-to-One with IPTVPlaylist
- One-to-Many with EPGProgram

#### EPGProgram
Represents a single program entry in the Electronic Program Guide.

**Fields**:
- `id: Long` - Primary key
- `channelId: Long` - Foreign key to IPTVChannel
- `title: String` - Program title
- `description: String?` - Program description (nullable)
- `startTime: Long` - Program start timestamp
- `endTime: Long` - Program end timestamp
- `category: String?` - Program category (nullable)
- `episodeNumber: Int?` - Episode number for series (nullable)
- `seasonNumber: Int?` - Season number for series (nullable)

**Relationships**:
- Many-to-One with IPTVChannel

### Debrid Entities

#### DebridAccount
Represents user's debrid service account configuration.

**Fields**:
- `id: Long` - Primary key
- `serviceType: String` - Service type (RealDebrid, Premiumize, AllDebrid)
- `apiKey: String` - Encrypted API key
- `username: String?` - Account username (nullable)
- `isActive: Boolean` - Whether account is currently active
- `lastUsed: Long` - Timestamp of last usage
- `quotaUsed: Long` - Used quota in bytes
- `quotaLimit: Long` - Total quota limit in bytes

**Relationships**:
- One-to-Many with TorrentContent

#### TorrentContent
Represents torrent-based content available through debrid services.

**Fields**:
- `id: Long` - Primary key
- `title: String` - Content title
- `description: String?` - Content description (nullable)
- `year: Int?` - Release year (nullable)
- `imdbId: String?` - IMDb identifier (nullable)
- `contentType: String` - Content type (Movie, TV Show, Episode)
- `quality: String` - Video quality (HD, 4K, SD)
- `size: Long` - File size in bytes
- `language: String` - Primary language
- `subtitles: List<String>` - Available subtitle languages
- `streamUrl: String?` - Debrid streaming URL (nullable)
- `infoHash: String` - Torrent info hash
- `seeders: Int` - Number of seeders
- `leechers: Int` - Number of leechers
- `source: String` - Source addon (Zilean, Mediafusion, Torrentio)
- `platform: String?` - Streaming platform (Netflix, Disney+, HBO, etc.) (nullable)
- `isFavorite: Boolean` - Whether content is marked as favorite
- `lastWatched: Long?` - Timestamp of last watch (nullable)
- `watchPosition: Long?` - Resume position in milliseconds (nullable)

**Relationships**:
- Many-to-One with DebridAccount

### User Data Entities

#### WatchHistory
Represents user's viewing history across both IPTV and debrid content.

**Fields**:
- `id: Long` - Primary key
- `contentType: String` - Content type (IPTV, Movie, TV Show)
- `contentId: String` - Reference to content (channel ID or torrent ID)
- `title: String` - Content title
- `watchedAt: Long` - Timestamp of viewing
- `duration: Long` - Total content duration in milliseconds
- `watchedDuration: Long` - Amount watched in milliseconds
- `source: String` - Content source (IPTV, Netflix, Disney+, etc.)

**Relationships**:
- No direct relationships (standalone entity)

#### Favorites
Represents user's favorite content from both IPTV and debrid sources.

**Fields**:
- `id: Long` - Primary key
- `contentType: String` - Content type (IPTV, Movie, TV Show)
- `contentId: String` - Reference to content
- `title: String` - Content title
- `addedAt: Long` - Timestamp when added to favorites
- `category: String?` - User-defined category (nullable)

**Relationships**:
- No direct relationships (standalone entity)

#### UserPreferences
Represents user's application preferences and settings.

**Fields**:
- `id: Long` - Primary key
- `key: String` - Preference key
- `value: String` - Preference value (JSON serialized)
- `updatedAt: Long` - Timestamp of last update

**Relationships**:
- No direct relationships (standalone entity)

### Search Entities

#### SearchHistory
Represents user's search history for quick access to recent searches.

**Fields**:
- `id: Long` - Primary key
- `query: String` - Search query
- `searchedAt: Long` - Timestamp of search
- `resultCount: Int` - Number of results returned

**Relationships**:
- No direct relationships (standalone entity)

## Validation Rules

### IPTVPlaylist
- `name` must not be empty and max 100 characters
- `url` must be valid HTTP/HTTPS URL
- `username` and `password` must be provided together if Xtream Code authentication is used
- `serverUrl` must be valid URL if provided
- `port` must be between 1 and 65535 if provided

### IPTVChannel
- `name` must not be empty and max 200 characters
- `url` must be valid stream URL
- `category` must not be empty and max 50 characters
- `country` must be valid ISO country code
- `quality` must be one of: SD, HD, 4K, UHD if provided

### TorrentContent
- `title` must not be empty and max 500 characters
- `contentType` must be one of: Movie, TV Show, Episode
- `quality` must be one of: SD, HD, 4K, UHD
- `size` must be positive
- `infoHash` must be valid SHA-1 hash (40 characters)
- `seeders` and `leechers` must be non-negative

### DebridAccount
- `serviceType` must be one of: RealDebrid, Premiumize, AllDebrid
- `apiKey` must not be empty and max 500 characters
- `quotaUsed` and `quotaLimit` must be non-negative

## State Transitions

### IPTVPlaylist States
- **INACTIVE** → **ACTIVE**: When playlist is successfully loaded and validated
- **ACTIVE** → **INACTIVE**: When playlist fails to load or user disables it
- **ACTIVE** → **UPDATING**: When playlist is being refreshed
- **UPDATING** → **ACTIVE**: When update completes successfully
- **UPDATING** → **INACTIVE**: When update fails

### TorrentContent States
- **AVAILABLE** → **STREAMING**: When user starts streaming content
- **STREAMING** → **AVAILABLE**: When streaming stops
- **AVAILABLE** → **EXPIRED**: When debrid link expires
- **EXPIRED** → **AVAILABLE**: When new debrid link is generated

### DebridAccount States
- **INACTIVE** → **ACTIVE**: When account is successfully authenticated
- **ACTIVE** → **INACTIVE**: When authentication fails or user disables account
- **ACTIVE** → **QUOTA_EXCEEDED**: When quota limit is reached
- **QUOTA_EXCEEDED** → **ACTIVE**: When quota resets or user upgrades

## Database Schema Considerations

### Indexing Strategy
- Primary keys on all entities
- Foreign key indexes on relationship fields
- Composite indexes on frequently queried fields:
  - IPTVChannel: (playlistId, category), (playlistId, isFavorite)
  - TorrentContent: (contentType, quality), (platform, contentType)
  - WatchHistory: (contentType, watchedAt), (contentId, watchedAt)

### Data Retention Policies
- WatchHistory: Keep last 1000 entries, older entries archived
- SearchHistory: Keep last 100 entries, older entries deleted
- EPGProgram: Keep only current and future programs, delete past programs older than 7 days

### Performance Optimizations
- Use Room database with proper indexing
- Implement pagination for large result sets
- Cache frequently accessed data in memory
- Use background threads for database operations
- Implement proper lifecycle management for database connections
