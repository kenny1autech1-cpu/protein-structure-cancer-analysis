# Protein Structure & Variant Analysis — FHL1 in Breast Cancer

> **Winter break project, 2026** · BSc Biochemistry & Data Science · University of Sydney

---

I built this over winter break to teach myself bioinformatics properly — not just copying tutorials, but understanding *why* each step works and what the data is actually saying.

The starting point was a breast cancer gene expression dataset I'd already analysed for a previous project. Four genes kept coming up as significantly downregulated in tumour tissue. I wanted to go deeper: what do these proteins actually look like, and does their shape explain why losing them is dangerous?

---

## The question

> Does AlphaFold's structural confidence predict where FHL1 mutations cause disease?

FHL1 is a tumour suppressor — a protein that normally keeps cell growth in check. When it's lost or mutated in breast cancer, cells start growing and migrating uncontrollably. I wanted to know: are all mutations equally bad, or do some regions tolerate change better than others?

---

## Where it started — 4 downregulated genes

My previous project identified four genes consistently downregulated in breast cancer (GSE42568 dataset, Affymetrix microarray). I downloaded AlphaFold structures for all four, visualised them in 3D, and compared their structural confidence profiles. FHL1 stood out immediately.

| Gene | What it does | Why it matters in cancer |
|------|-------------|--------------------------|
| **FHL1** | Scaffold protein | Tumour suppressor; loss allows cells to grow and migrate freely |
| **PDE3B** | Breaks down cAMP; controls fat metabolism | Loss disrupts metabolic reprogramming |
| **ACSM5** | Activates fatty acids | Loss rewires fat metabolism to fuel tumour growth |
| **VGLL3** | Transcription regulator | Loss dysregulates gene expression programs |

**👉 [View all 4 proteins as interactive 3D structures](https://kenny1autech1-cpu.github.io/protein-structure-cancer-analysis/)** — rotate, zoom, coloured by structural confidence.

---

## The finding that drove everything

FHL1 had a cliff edge at residue 230. Everything before it — the LIM domains — is well structured. Everything after it is a floppy, unstructured tail with no fixed shape. FHL2, FHL3, and FHL4 don't have this tail at all.

| Gene | Avg pLDDT | Structured (>90%) | Disordered (<50%) |
|------|-----------|-------------------|-------------------|
| FHL1 | 73.1 | 40.4% | 26.4% |
| FHL2 | 92.3 | 81.5% | 0.0% |
| FHL3 | 91.8 | 79.3% | 0.4% |
| FHL4* | 92.2 | 81.3% | 0.0% |

*FHL4 is mouse — human FHL4 isn't in AlphaFold yet.*

So the hypothesis: **mutations in the structured LIM domains should be damaging. Mutations in the disordered tail should be tolerated.** I tested this with two more independent datasets.

---

## Three layers of evidence

**AlphaFold pLDDT** — confidence collapses at residue 230 and stays low to the end.

**AlphaMissense** — DeepMind's model scored all 6,137 possible FHL1 missense mutations. LIM domains are almost entirely red (damaging). The disordered tail is almost entirely blue (tolerated). Same boundary, completely independent method.

**ClinVar** — real patient variants fetched via NCBI Entrez API, remapped to the canonical isoform. Four confirmed pathogenic variants recovered at positions 94, 216, 268, and 310.

---

## What I learned

- How AlphaFold stores confidence in PDB files (B-factor column, positions 60–66 of every ATOM line)
- How to stream a 1.2GB gzip without loading it into memory
- Why isoform mismatches between databases cause silent bugs
- The esearch → efetch pattern for querying NCBI
- That disordered proteins aren't broken — they're often disordered by design

---

## Limitations

- FHL4 is mouse (*Mus musculus*) — human FHL4 not in AlphaFold
- ClinVar and AlphaMissense use different FHL1 isoforms; remapped via RefSeq NP_ accession matching
- Only 4 ClinVar variants recovered — limited clinical data for FHL1
