# Project Checkpoint — FHL Protein Structure Analysis

**Date:** July 6, 2026

---

## What you've done

### 1. Extracted pLDDT confidence scores from AlphaFold PDB files
- Learned how PDB files are structured (ATOM lines, B-factor column at positions 60–66)
- Wrote a Python loop to parse all 4 FHL proteins

### 2. Downloaded AlphaFold structures
- FHL1: already named `FHL1.pdb`
- FHL2: `Q14192.pdb` (UniProt ID)
- FHL3: `Q13643.pdb`
- FHL4: `Q8CDC8.pdb` (corrected from Q5T012)

### 3. Results table

| Gene | Avg pLDDT | >90% conf | <50% disord |
|------|-----------|-----------|-------------|
| FHL1 | 73.1      | 40.4%     | 26.4%       |
| FHL2 | 92.3      | 81.5%     | 0.0%        |
| FHL3 | 91.8      | 79.3%     | 0.4%        |
| FHL4 | 92.2      | 81.3%     | 0.0%        |

### 4. Validated against literature
- FHL1 disorder confirmed by: unique alternative splicing (3 isoforms), MAPK scaffolding function
- FHL2/3/4 high structure confirmed by AlphaFold entry (92.06 shown on website = 92.3 computed)
- Sources: PMC6082310, PMC3822721, PMC7309467

---

## Key concepts learned
- AlphaFold uses UniProt accession IDs, not gene names
- pLDDT > 90 = high confidence / well structured
- pLDDT < 50 = likely disordered (no fixed 3D shape)
- Scaffold proteins are often disordered by design (flexibility = function)

---

## Next steps (in order)
1. ~~**Visualise pLDDT along the sequence**~~ ✓ Done — FHL1 disordered tail confirmed at residues 230–325
2. ~~**Species consistency check**~~ ✓ Done — FHL1/2/3 are human, FHL4 is mouse (noted as limitation)
3. **Gene expression analysis** — download GSE42568, run differential expression (starting next)

---

## Files in data/
- `FHL1.pdb`, `Q14192.pdb`, `Q13643.pdb`, `Q8CDC8.pdb` — AlphaFold structures
- All other .pdb files — other proteins in the dataset (not yet analysed)
