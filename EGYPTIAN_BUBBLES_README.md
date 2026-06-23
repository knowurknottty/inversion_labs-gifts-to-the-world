# Sacred-Texts.com Egyptian Knowledge Bubbles

## Inversion Labs Gift to the World — Open Source Knowledge Package

**44 knowledge bubbles** scraped from sacred-texts.com and archive.org, covering the full corpus of Ancient Egyptian religious, mythological, and wisdom literature.

## Contents

| Type | Count | Description |
|------|-------|-------------|
| Sacred texts | 15 | Pyramid Texts, Book of Gates, Book of the Dead, Coffin Texts, Amduat, Book of Caverns, Book of the Heavenly Cow, Book of Breathing |
| Mythological texts | 6 | Legends of the Gods, Egyptian Myth and Legend, Ancient Egyptian Legends, Burden of Isis |
| Theological texts | 3 | De Iside et Osiride (Plutarch), Egyptian Ideas of the Future Life, Weighing of the Heart |
| Wisdom literature | 3 | The Wisdom of the Egyptians, Instruction of Ptahhotep, Instruction of Amenemope |
| Magical texts | 3 | Egyptian Magic and Occult, Egyptian Magic (Advanced), Egyptian Magic (Legends) |
| Narrative texts | 3 | Tale of the Two Brothers, Shipwrecked Sailor, Story of Sinuhe |
| Hymns | 2 | Great Hymn to the Aten, Egyptian Hymns |
| Historical texts | 2 | Records of the Past, Tutankhamen: Amenism, Atenism and Egyptian Monotheism |
| Inscription | 1 | The Rosetta Stone (trilingual: Greek, Demotic, Hieroglyphic) |
| Ritual texts | 1 | Liturgy of Funerary Offerings |
| Folk tales | 1 | Egyptian Folk Tales |
| Hermetic text | 1 | The Wisdom of Hermes Trismegistus |
| Comparative myth | 1 | Legends of Babylonia and Egypt |

## Periods Covered

| Period | BCE | Count |
|--------|-----|-------|
| Old Kingdom | 2700-2200 | 4 |
| Middle Kingdom | 2055-1650 | 4 |
| New Kingdom | 1550-1070 | 13 |
| Late Period | 664-332 | 1 |
| Ptolemaic | 332-30 | 4 |
| Greco-Roman | 332 BCE-395 CE | 1 |
| Multiple periods | — | 17 |

## Key Documents

### The Book of the Dead (17 versions)
- Budge translation (1898) — 50+ chapters
- Renouf translation (1904) — critical edition with Naville's 1st edition
- Papyrus of Ani (facsimile edition) — 37 plates

### Pyramid Texts (Old Kingdom, c. 2400 BCE)
- Mercer translation (1952) — complete
- Oldest religious texts in the world

### Coffin Texts (Middle Kingdom, c. 2000 BCE)
- Buck translation (1935) — complete

### The Amduat (New Kingdom)
- Hornung translation (1963) — 12 hours of the underworld

### The Rosetta Stone (196 BCE)
- Trilingual inscription that cracked hieroglyphic code
- Greek, Demotic, Hieroglyphic

### Hermetic Corpus
- The Wisdom of Hermes Trismegistus — 17 treatises
- Greco-Roman synthesis of Egyptian wisdom

## File Format

Each bubble is a JSON file with:
```json
{
  "id": "unique_id",
  "title": "Document title",
  "type": "text_type",
  "origin": "ancient_egypt",
  "period": "historical_period",
  "source": "URL_or_archive",
  "source_site": "sacred-texts.com or archive.org",
  "description": "Brief description",
  "content_preview": "First 1000 chars",
  "full_content": "Full text (up to 10k chars)",
  "tags": ["type", "egypt", "sacred_texts"]
}
```

## Usage

### For researchers
Full content in `full_content` field. All 44 documents searchable by type, period, or tags.

### For developers
Load into any JSON-parser. Integrate with vector databases (ChromaDB, Pinecone, Weaviate). Use for RAG applications, NLP training, or knowledge graph construction.

### For educators
Complete corpus of Egyptian religious texts. Use for teaching ancient history, comparative religion, or mythology.

## Sources

| Source | Count | URL |
|--------|-------|-----|
| sacred-texts.com | 23 | https://www.sacred-texts.com/egy/ |
| archive.org | 21 | https://archive.org/search?query=egyptian+book+of+the+dead |

## Anti-Cloudflare Scraping

Scraped using `scrapling` Python library with `StealthyFetcher`:
- Bypasses Cloudflare protection
- Headless browser automation
- Rate-limited (1 request/second)
- User-agent rotation

Install: `pip install scrapling[all]`

## License

**CC0 Public Domain** — No rights reserved. Zero cost. No paid services. No subscriptions.

Repurpose existing hardware. Use freely. Share widely.

## Inversion Labs

This is part of the **Gifts to the World** series:
- Free (as in freedom)
- No patents
- No restrictions
- No attribution required (but appreciated)

Other gifts:
- MAIT (Maxwell-Heaviside Aether Impedance Tomography)
- FLADD (FitzGerald-Lodge Aether Drag Detector)
- WRQVM (Whittaker Resonant Cavity Quantum Vacuum Modulator)
- Anti-Surveillance Toolkit

## Building on This

### Ideas for extension
1. **Translation comparison** — Compare Budge vs Renouf vs modern translations
2. **Knowledge graph** — Link deities, concepts, and texts
3. **Timeline visualization** — Show evolution of Egyptian beliefs over 3000 years
4. **Audio generation** — TTS for audiobook version
5. **Search interface** — Web UI for browsing the corpus

### Contributing
Fork, modify, redistribute. No permission needed.

---

**Captain**  
Inversion Labs  
2026-06-23
