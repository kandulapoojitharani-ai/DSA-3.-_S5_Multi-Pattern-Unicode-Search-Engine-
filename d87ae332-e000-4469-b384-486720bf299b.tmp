# Multi-Pattern Unicode Search Engine Using Aho–Corasick Algorithm (TextHack)

**Course:** Data Structures and Algorithms-3 (25CS2103E), A.Y. 2026-2027
**Department:** Computer Science and Engineering, KL Deemed to be University (KLH), Hyderabad

TextHack is a menu-driven, console-based Java application. Its main feature is a Unicode-aware multi-pattern search engine built on the **Aho–Corasick** algorithm: a Trie of all keywords plus failure links, so the text is scanned **once** for all keywords instead of once per keyword. The same program also demonstrates algorithms from the other DSA-3 modules (KMP, edit distance, LCS, max-flow, matching, approximation, scheduling, Miller–Rabin and prefix scan).

---

## Team

| Name | Roll No. |
|---|---|
| Kandula Poojitha Rani | 2520030460 |
| Himesh | 2520030317 |
| Ishwak | 2520030458 |

**Team Number:** 9
**Guide:** Swati D, Assistant Professor, Department of CSE

---

## Features

- **Unicode multi-pattern search (Aho–Corasick):** up to 500 patterns at once, matched against every stored document. Reports document ID, pattern, start index and end index for every occurrence, including overlapping ones.
- **Unicode support:** text and patterns are processed as Unicode code points (`String.codePoints()`), so English, Indian languages, Asian languages and symbols work, and positions are reported as code-point indices.
- **Single-pattern search (KMP)** with an LPS table.
- **Fuzzy search** using Wagner–Fischer edit distance.
- **Document comparison** using LCS and a similarity percentage.
- **Algorithm demos:** Edmonds–Karp max-flow, bipartite matching, vertex-cover 2-approximation, deadline-order scheduling, Miller–Rabin primality test, Blelloch prefix scan.

---

## Menu Options

| # | Option | Algorithm | Complexity reported by the program |
|---|---|---|---|
| 0 | API overview | , | , |
| 1 | Add your own document | , | , |
| 2 | View stored documents | , | , |
| 3 | Unicode multi-pattern search | Aho–Corasick | O(N + Z) after preprocessing |
| 4 | KMP single-pattern search | Knuth–Morris–Pratt | O(n + m) |
| 5 | Fuzzy search across documents | Wagner–Fischer DP | O(n · m) per comparison |
| 6 | Compare two documents | Longest Common Subsequence DP | O(n · m) |
| 7 | Maximum flow | Edmonds–Karp | O(V · E²) |
| 8 | Bipartite matching | Augmenting paths | , |
| 9 | Vertex-cover approximation | 2-approximation | at most 2 × optimal |
| 10 | Scheduling demonstration | Deadline-order heuristic | heuristic only |
| 11 | Miller–Rabin primality test | Randomized (10 rounds) | probabilistic |
| 12 | Prefix scan | Blelloch scan | O(n) work |
| 13 | Exit | , | , |

---

## How the Aho–Corasick Engine Works

**Phase 1: preprocessing**
1. Convert every pattern to Unicode code points.
2. Insert all patterns into a **Trie**; the last node of each pattern stores that pattern's ID in its output list.
3. Run a **BFS** over the Trie to compute **failure links**, and merge each node's failure-link outputs into its own output list so that patterns that are suffixes of other matches are also reported.

**Phase 2: search**
1. Read the text left to right, one code point at a time.
2. Follow the Trie edge for the code point; if none exists, follow failure links until an edge is found or the root is reached.
3. At every node reached, report all patterns in its output list.

The text is never re-read, and the Trie is built once and reused for every stored document.

---

## Requirements

- **Java JDK 8 or later** (the code uses `String.codePoints()`)
- Any Java IDE, or a terminal with `javac` and `java`
- A UTF-8 enabled terminal if you want to test non-English text

---

## How to Run

```bash
# 1. Put the source in Main.java (the class is named Main)
javac Main.java

# 2. Run
java Main
```

On Windows, if Telugu/Hindi text shows as `?`, switch the console to UTF-8 first (`chcp 65001`) or run with `java -Dfile.encoding=UTF-8 Main`.

### Typical workflow

1. Choose `1` and type a document. Finish with `END` on its own line.
2. Choose `3` to run the multi-pattern search, enter how many patterns, then each pattern.
3. Read the matches and total.
4. Choose `13` to exit.

---

## Sample Output

### Multi-pattern search (option 3)

Document (option 1): `ushers are using he and she.`
Patterns: `he`, `she`, `his`, `hers`

```
Document 0 | Pattern: he | Start: 2 | End: 3
Document 0 | Pattern: she | Start: 1 | End: 3
Document 0 | Pattern: hers | Start: 2 | End: 5
Document 0 | Pattern: he | Start: 17 | End: 18
Document 0 | Pattern: he | Start: 25 | End: 26
Document 0 | Pattern: she | Start: 24 | End: 26
Total matches: 6
Algorithm: Aho-Corasick
Search complexity: O(N + Z), after preprocessing
```

`he` and `she` end at the same position, and both are reported. Indices are zero-based and the end index is inclusive.

### KMP search (option 4)

Taken from the project's run screenshot: searching for `meaningful` in the introduction paragraph gives

```
Match at code-point index 833
Total matches: 1
Time complexity: O(n + m)
```

### Other demos

```
Maximum flow: 23                              (option 7)

Maximum matching size: 3                      (option 8)
Left 0 -> Right 0
Left 2 -> Right 1
Left 1 -> Right 2

Approximate vertex cover: 0 1 2 3 4 5         (option 9, optimal size is 3)

Index: finish=2, deadline=4 (on time)         (option 10)
Corpus: finish=5, deadline=5 (on time)
Testing: finish=7, deadline=8 (on time)
Search: finish=11, deadline=10 (late)
Report: finish=12, deadline=12 (on time)
```

The max-flow, matching, vertex-cover and scheduling demos use fixed example data built into the program.

---

## Complexity

Let **P** = total code points across all patterns, **N** = text length, **Z** = number of reported matches.

- **Time:** O(P + N + Z)
- **Space:** about O(P) for the Trie, failure links and output lists (the Trie uses linked edge lists, which suit the very large Unicode alphabet better than a dense table).

---

## Applications

Search engines, intrusion detection, spam and malware detection, plagiarism checking, keyword monitoring, content moderation, log monitoring, digital libraries and multilingual information retrieval.

---

## Limitations

- Exact matching only: no spelling-mistake, synonym or transliteration handling in the Aho–Corasick search (the fuzzy search in option 5 works word by word).
- Documents live in memory only (maximum 100) and are lost when the program exits.
- Text is typed in at the console; there is no file upload yet.
- No Unicode normalization (for example NFC) or case folding in the multi-pattern search, so visually identical text with different code-point sequences will not match.
- Positions are code-point indices, not byte offsets.
- The prefix scan is a sequential demonstration of a parallel algorithm.
- The scheduling demo is a heuristic, not an optimal scheduler.
- The matching, max-flow, vertex-cover and scheduling demos use hard-coded inputs.

## Future Scope

- Graphical or web interface
- File and dataset input for large corpora
- Compact (array-based or double-array) tries to reduce memory
- Multi-threaded scanning and a truly parallel prefix scan
- Unicode normalization, case folding and grapheme-cluster awareness
- Integration with intrusion detection, spam filtering and plagiarism checking, plus benchmarks against repeated KMP

---

## Reference

A. V. Aho and M. J. Corasick, "Efficient string matching: an aid to bibliographic search", *Communications of the ACM*, 1975.
