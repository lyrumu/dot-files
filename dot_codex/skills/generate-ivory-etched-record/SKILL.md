---
name: generate-ivory-etched-record
description: Generate restrained music-themed images featuring a tactile warm-ivory record or circular disc with a same-material bas-relief instrument engraving. Use when the user asks for the distinctive pale carved-disc texture from lyrumu's README reference; do not trigger for generic music graphics or ordinary black vinyl.
---

# Generate Ivory Etched Record

Create images whose signature object is a pale physical disc combining fine record grooves with a shallow carved instrument relief. Preserve the user's requested subject, composition, copy, and output format; this skill governs the disc's material language, not the whole layout.

## Reference

Use [assets/ivory-etched-record-reference.png](assets/ivory-etched-record-reference.png) as a **material and lighting reference** whenever image input is supported. Do not copy its README layout, avatar, text, or navigation unless the user asks for them.

Text alone is less reliable than the reference image. Attach the reference on the first generation and retain it during refinements.

## Material signature

Describe the object with these coupled traits:

- A thick circular record-like disc made from warm ivory stone, matte porcelain, or fine plaster; never black vinyl.
- Fine concentric grooves remain visible across the face, with slight natural irregularity rather than perfect vector rings.
- A violin, cello, or user-specified instrument is carved as a **very shallow same-material bas-relief** emerging from the disc surface.
- The instrument is monochrome and integrated into the disc: raised edges, recessed seams, delicate tool marks, and soft occlusion in the carving.
- A small spindle hole and restrained beveled rim make the disc feel manufactured yet sculptural.
- Warm off-white values remain close together. Form is revealed by light and micro-shadow, not by strong outlines or added color.

## Light and framing

- Use a large diffused key light from the upper-left or upper-front at a shallow angle.
- Add soft ambient fill and one narrow contact shadow below/right of the disc.
- Keep highlights matte and broad; retain detail in whites without blown-out areas.
- Prefer a straight-on or lightly elevated product-study view with generous negative space.
- Let the disc be the sole visual focus unless the user supplies another hierarchy.

## Default exclusions

Avoid glossy plastic, metallic CD reflections, black vinyl, colored instruments, printed illustrations, stickers, deep-cut stone relief, detached floating instruments, heavy outlines, dramatic shadows, ornate frames, floating music-note glyphs, extra text, logos, and watermarks.

Do not use named consumer-brand styles as shorthand. Express the actual material, light, spacing, and contrast requirements instead.

## Prompt construction

Use the user's requested asset type and subject, then incorporate this core block:

```text
Signature object: a warm-ivory stone/porcelain record disc with fine concentric grooves, a restrained beveled edge, and a small spindle hole. A [INSTRUMENT] is integrated into the face as a shallow same-material bas-relief, with delicate carved edges, subtle recessed seams, faint tool marks, and realistic micro-occlusion. Large diffused upper-left light, soft ambient fill, narrow contact shadow below-right, matte highlights, low-contrast warm whites, generous negative space. The result must read as a photographed physical sculpture, not a flat illustration.

Avoid: black vinyl, metallic or rainbow reflections, glossy plastic, colored or printed instrument, detached object, deep relief, heavy outline, hard shadow, floating music notes, extra text, logo, watermark.
```

Add exact text separately and quote it verbatim. Do not add copy the user did not provide.

## Quality check

Before accepting the result, verify all four:

1. The disc reads as a physical ivory object with thickness, grooves, and a restrained rim.
2. The instrument reads as part of the same material, not a picture placed on top.
3. Low-contrast details remain legible through grazing light and micro-shadow.
4. No stray note glyphs, invented text, glossy vinyl cues, or dark dramatic effects appear.

If one criterion fails, refine only that defect while retaining both the reference and the latest acceptable image. Do not regenerate the whole visual direction unnecessarily.
