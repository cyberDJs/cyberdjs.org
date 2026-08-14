# Content Model — CyberDJs.org

Suggested structures. Implement as TypeScript objects, JSON, MDX, CMS documents or another source depending on the chosen stack.

## Artist

```ts
type Artist = {
  id: string
  name: string
  role?: string
  shortBio: string
  genres: string[]
  location?: string
  image?: string
  links: {
    website?: string
    soundcloud?: string
    spotify?: string
    instagram?: string
    youtube?: string
    mixcloud?: string
    booking?: string
  }
  featuredMixIds?: string[]
}
```

## Music item

```ts
type MusicItem = {
  id: string
  title: string
  artistIds: string[]
  type: 'mix' | 'release' | 'playlist' | 'video'
  platform: 'soundcloud' | 'spotify' | 'apple' | 'youtube' | 'mixcloud' | 'other'
  url: string
  embedUrl?: string
  date?: string
  description?: string
}
```

## Event

```ts
type Event = {
  id: string
  title: string
  date: string
  city?: string
  country?: string
  venue?: string
  artistIds?: string[]
  url?: string
  status: 'upcoming' | 'past' | 'cancelled'
}
```

## Project

```ts
type Project = {
  id: string
  title: string
  tagline: string
  description: string
  status: 'idea' | 'prototype' | 'active' | 'archived'
  links?: {
    repo?: string
    demo?: string
    docs?: string
  }
  tags: string[]
}
```

## Booking inquiry

Preferred fields:

- name
- email
- organization
- event type
- event date
- location
- expected audience size
- budget range optional
- message

Validate inputs and protect against spam.

## Provisional copy

Hero line options:

- `CyberDJs — underground signal for future dancefloors.`
- `An artist crew wired for sound, code and controlled chaos.`
- `DJs, producers and music-tech experiments from the edge of the booth.`

Manifesto fragments:

- `We play records, break systems and build the tools we wish existed.`
- `No autoplay. No template cult. No corporate fog machine.`
- `Human instinct amplified by machines, not replaced by them.`

Mark all owner-verification content clearly before launch.
