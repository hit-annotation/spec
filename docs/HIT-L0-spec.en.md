# HIT Annotation Specification `L0` (Label Notation) v0.1.1

> **HIT label of this document:** `HIT-C9/L10-SPORT`
>
> | Item | Content |
> | --- | --- |
> | AI used | Anthropic Claude Opus 5.5 |
> | Created | 2026-11-15 |
> | M attribute | C9: Based on the declarant's draft and instructions, AI created the full text, and the declarant revised it. L10: AI translated the entire text from the Japanese original. |
> | T attribute | S, P, O, R, T (see "Appendix A: Disclosed Materials for This Document") |
> | Original label (Japanese version) | `HIT-C9-SPORT` |
>
> **License:** This document is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
>
> © 2026 Youmei Masada

---

## 0. Document Information

| Item | Content |
| --- | --- |
| Title | HIT Annotation Specification L0 (Label Notation) |
| Version | 0.1.1 (Proposal) |
| Status | Draft. The rules and normative content may change. |
| Scope | Declaration level L0. L1 and L2 will be specified in separate documents. |
| Language | This document is an English translation of the Japanese original. If the two versions differ, the Japanese version prevails. |

---

## 1. Overview

### 1.1 Names

| Category | Name |
| --- | --- |
| Official name | Human Indication and Traceability (HIT) Annotation |
| Japanese name | 人跡証憑 (short form: 人証) |
| Identifier used in labels | `HIT` |

### 1.2 Purpose

The purposes of this specification are as follows.

1. **Building a human chain of trust:** Only people (natural persons or legal entities) can be legal subjects. This specification promotes the fair use of AI while helping to re-establish the foundations of intellectual property in the age of AI. To this end, it builds a "human chain of trust" that identifies the origin of content, based on copyright concepts that are highly compatible across countries.
2. **Protecting human creativity:** AI output continuously exposes culture to algorithmic interference. This specification aims to prevent spontaneous human creativity from being damaged without limit as a result, whether unintentionally or deliberately.
3. **Promoting discussion on the distribution of compensation:** This specification presents a norm for distinguishing results based on the use of AI from the intellectual work of individuals or legal entities. In this way, it promotes discussion on the distribution of compensation among copyright management organizations and rights managers in each country.
4. **Distinguishing the capabilities of AI from those of humans:** This specification makes it possible to determine which parts of content depended on which AI, and what changes the author made.

### 1.3 Nature of This Specification

1. HIT is a self-declaration standard.
2. HIT does not define the rights or obligations of the declarant. Rights and obligations are determined by the individual licenses or contracts that apply to the target content.
3. This specification defines the following two things:
   - The syntax and meaning of labels (Chapters 4 to 8)
   - Practices recommended for declarants (Chapter 9)

---

## 2. Terms and Normative Language

### 2.1 Terms

| Term | Definition |
| --- | --- |
| Declarant | The natural person or legal entity that attaches a HIT label |
| Target content | The work to which a HIT label is attached (documents, images, audio, video, software, and so on) |
| AI | A generative algorithm based on a trained model |
| Involvement | The reflection of AI output in the target content |
| Degree | An integer from 1 to 10 that expresses the extent of involvement |
| Disclosed materials | Information provided together with the target content, as indicated by T-attribute flags |
| Recipient | A person who lawfully receives the target content |
| Profile | An additional set of rules that supplements the operation of this specification for a specific jurisdiction |

### 2.2 Normative Language

This specification uses the following expressions with the meanings below. The English keywords are interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

| Japanese | English | Meaning |
| --- | --- | --- |
| しなければならない | MUST | A requirement for a label to conform to this specification |
| してはならない | MUST NOT | A prohibition for a label to conform to this specification |
| すべきである | SHOULD | A recommendation to be followed unless there is a valid reason not to |
| すべきではない | SHOULD NOT | A recommendation to avoid unless there is a valid reason not to |
| してもよい | MAY | An optional item |

These expressions define the conformance of labels. They do not impose legal obligations on the declarant.

---

## 3. Design Principles

1. **Self-declaration, not legal judgment:** A declaration is a statement of fact. It does not determine copyrightability or the ownership of rights.
2. **License neutrality:** HIT does not replace existing license systems. It is an auxiliary layer placed on top of them.
3. **Jurisdiction neutrality:** The core vocabulary does not depend on the legal concepts of any specific country. Interpretations for each jurisdiction are separated into profiles.
4. **Incremental adoption:** HIT can be used anywhere from a human-readable label alone to signed, machine-readable proof.
5. **Minimal enforcement:** The scope of disclosure is optional. HIT does not require the disclosure of trade secrets or personal information. It does not interfere with patent rights or other intellectual property rights.
6. **Declarations start from people:** The declarant is always a person (a natural person or a legal entity).

---

## 4. Label Syntax

### 4.1 Basic Structure

A HIT label has the following structure.

```text
HIT-<M attribute>-<T attribute>
or
HIT-<M attribute>
```

1. The prefix is `HIT`.
2. The prefix, M attribute, and T attribute are separated by a hyphen-minus `-` (U+002D).
3. The M attribute MUST NOT be omitted.
4. The T attribute may be omitted only when no traceability information is provided.
5. A label without a T attribute is equivalent to a label with `N` as its T attribute.

### 4.2 Additional Syntax Rules

1. Flags are written in uppercase letters.
2. A HIT label MUST consist only of ASCII uppercase letters, digits, the hyphen-minus `-`, and the slash `/`.
3. The same flag MUST NOT appear more than once within one attribute.
4. A label MUST NOT contain spaces.
5. Declarants SHOULD write flags in the following canonical order. Parsers SHOULD accept other orders.
   - M attribute: `C`, `D`, `A`, `L`
   - T attribute: `S`, `P`, `O`, `R`, `T`, `V`

---

## 5. M Attribute (Modification: Type and Degree of Involvement)

The M attribute expresses the type and degree of AI involvement in the target content. The type of involvement is expressed by a flag, and the degree of involvement by a degree value.

### 5.1 Flags

| Flag | Name | Meaning | Degree | Corresponding IPTC Digital Source Type (informative) |
| --- | --- | --- | --- | --- |
| `C` | Co-creation | AI created the content based on a human concept, or a human and AI created it together. | Required | [compositeWithTrainedAlgorithmicMedia](http://cv.iptc.org/newscodes/digitalsourcetype/compositeWithTrainedAlgorithmicMedia) |
| `D` | Delegated concept | The concept was delegated to AI, and a human gave further instructions and made selections. | Required | [trainedAlgorithmicMedia](http://cv.iptc.org/newscodes/digitalsourcetype/trainedAlgorithmicMedia) |
| `A` | Amendment | AI corrected, edited, or partially revised an original work made by a human. | Required | [algorithmicallyEnhanced](http://cv.iptc.org/newscodes/digitalsourcetype/algorithmicallyEnhanced) |
| `L` | Translation | AI translated an original work. | Required | [algorithmicallyEnhanced](http://cv.iptc.org/newscodes/digitalsourcetype/algorithmicallyEnhanced) |
| `H` | Human-made | There is no AI involvement. | Not attached | [digitalCreation](http://cv.iptc.org/newscodes/digitalsourcetype/digitalCreation) |

The correspondence with IPTC Digital Source Type is informative. It is intended for use in L1 machine-readable metadata.

### 5.2 Combination Rules

1. `H` MUST NOT be combined with any other M-attribute flag.
2. `C` and `D` MUST NOT be combined with each other.
3. `A` may be combined with any of `C`, `D`, and `L`.
4. `L` may be combined with any of `C`, `D`, and `A`.

| | `C` | `D` | `A` | `L` | `H` |
| --- | --- | --- | --- | --- | --- |
| `C` | — | ✘ | ✅ | ✅ | ✘ |
| `D` | ✘ | — | ✅ | ✅ | ✘ |
| `A` | ✅ | ✅ | — | ✅ | ✘ |
| `L` | ✅ | ✅ | ✅ | — | ✘ |
| `H` | ✘ | ✘ | ✘ | ✘ | — |

### 5.3 Degree

1. The degree expresses, on a 10-step scale, the share of the whole target content that received the involvement indicated by the flag. `1` means about 10%, and `10` means the whole.
2. The degree is an integer from 1 to 10 inclusive.
3. The declarant chooses the basis for calculating the share (number of characters, number of lines, playback time, area, and so on). The declarant MAY state the basis of calculation.
4. Fractions are rounded to the nearest integer. However, if there is involvement and the share is less than 10%, the degree is `1`. If the share is less than 100%, the degree is `9` at most.
5. When multiple flags are used, the degree is calculated independently for each flag. The sum of the degrees may exceed 10.

Example: `C3/L10` means that AI created about 30% of the content and also translated the entire text.

---

## 6. T Attribute (Traceability)

The T attribute expresses the types of information provided for tracing how the target content was produced. T-attribute flags take no degree.

### 6.1 Flags

| Flag | Name | Meaning |
| --- | --- | --- |
| `S` | System prompt | The system prompt that the declarant set, or was able to obtain, is disclosed. Parts the declarant cannot obtain (such as non-public parts set by the platform operator) need not be included in the disclosed materials. However, the declarant SHOULD state this. |
| `P` | Prompts and responses | The full text of the prompts used for generation (excluding the system prompt) and the full text of the AI's response to each prompt are disclosed. |
| `O` | Original | The original work, or the AI-generated content before editing, is disclosed. |
| `R` | References | A list of the documents and materials given to the AI or consulted by the AI is disclosed. |
| `T` | Timestamps | The dates or dates and times of generation and editing are disclosed. |
| `V` | Verification | The model used for generation and the creator can be proven by digital signature or digital watermark. |
| `N` | None | No information for tracing is provided. MUST NOT be combined with other flags. |

1. When `P` is attached, the disclosed materials MUST include not only the declarant's instructions but also the full text of the AI's responses. The responses include output that was not adopted in the target content.
2. At L0, `V` is a statement that a means of proof exists. The method of verifying the proof will be specified in L2.

### 6.2 When the M Attribute Is `H`

1. Because there is no AI generation process, `S`, `P`, and `O` MUST NOT be attached.
2. `R`, `T`, `V`, and `N` may be attached.

### 6.3 Meaning and Scope of Disclosure

1. In this specification, "disclosure" means making the disclosed materials available to recipients. It does not necessarily mean publication to the general public.
2. When recipients are limited to the parties to a contract (for example, provision under a non-disclosure agreement), disclosure to that extent is sufficient.
3. The declarant MAY exclude trade secrets, personal information, and information that may infringe the rights of third parties from the disclosed materials. In this case, the declarant SHOULD indicate that information was excluded and where.

---

## 7. Label Examples

### 7.1 Conforming Labels

| Label | Meaning |
| --- | --- |
| `HIT-C4-N` | A co-creation in which AI created about 40% based on a human concept, and the declarant created and edited the rest. No traceability information is provided. |
| `HIT-A1/L10-POR` | AI revised about 10% of an original work created by the declarant and translated the entire text. The full text of the prompts (excluding the system prompt) and AI responses, the original work and the AI-generated content before editing, and a list of references are attached. |
| `HIT-C10-SP` | AI created the entire text, and the declarant reviewed all of it without making changes. The full text of the system prompt, prompts, and AI responses is attached. (Whether a review took place cannot be expressed in the label, so it is stated in the accompanying information.) |
| `HIT-D10-PT` | The concept was delegated to AI, and the entire text was created through the declarant's instructions and selections. The full text of the prompts and AI responses, and the creation date or date and time, are disclosed. |
| `HIT-H-TV` | A human created the content, with no AI involvement. The creation date and time are disclosed, and the creator can be proven by digital signature. |
| `HIT-H-N` | A human created the content, with no AI involvement. No traceability information is provided. |

### 7.2 Non-conforming Labels

| Label | Reason |
| --- | --- |
| `HIT-H/A2-N` | `H` and `A` cannot be combined (5.2). |
| `HIT-H3-N` | `H` takes no degree (5.1). |
| `HIT-C11-N` | The maximum degree is 10 (5.3). |
| `HIT-S` | The M attribute cannot be omitted (4.1). |
| `HIT-H-SP` | When the M attribute is `H`, `S` and `P` cannot be attached (6.2). |
| `HIT-C4-PN` | `N` cannot be combined with other flags (6.1). |

---

## 8. Display at L0

### 8.1 Position

1. A HIT label MUST be displayed where recipients can notice it during normal viewing.
2. A HIT label SHOULD be written as copyable text. It SHOULD NOT be shown only as text inside an image.
3. The recommended positions are as follows:
   - Documents: at the beginning or end, near the license notice
   - Images, audio, and video: in the caption, credits, or description
   - Software: in a comment at the top of source files, or in an accompanying document such as a README

### 8.2 Accompanying Information

The declarant SHOULD state the following items together with the HIT label, or separately at the beginning or end of the content.

```text
HIT-<label>
AI: <provider> <model>[, <provider> <model> ...]
Created: <YYYY-MM-DD>[T<hh:mm>(Z|±<hh:mm>)]
Disclosures: <location>
```

1. The creation date, or date and time, is written in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.
2. The declarant MAY also state the following items as needed:
   - The basis for calculating the degree
   - Whether any information was excluded from the disclosed materials, and where
   - Whether a human review took place
   - The original label (8.4)

### 8.3 Labels for Parts

1. When AI involvement differs between parts of the target content, a HIT label MAY be attached to each part.
2. Even when labels are attached to parts, a HIT label for the target content as a whole SHOULD be attached.

### 8.4 Labels for Derivative Works

1. A person who modifies content that carries a HIT label SHOULD attach a new HIT label to the modified content as a whole.
2. The HIT label before modification SHOULD be stated as the "original label".

---

## 9. Normative Practices (Recommended)

The following are ethical and normative practices recommended for declarants.

1. The degree of the M attribute should be the closest approximation of the actual involvement.
2. When the extent of involvement is hard to judge, estimate it on the higher side rather than the lower side.
3. When any of `S`, `P`, `O`, `R`, `T`, or `V` is attached to the T attribute, embed the disclosed materials in the target content or distribute them together with the target content.
4. State the provider name and model name of every AI used, and the dates and times when prompts were entered, together with the HIT label.
5. When the target content is updated, also update the HIT label and the disclosed materials.

---

## 10. Relationship with Existing Licenses

### 10.1 General Principles

1. A HIT label is not a license. It does not add to or change the terms of any license.
2. A HIT label does not replace a license notice. It is displayed alongside the license notice.
3. If a HIT label appears to conflict with the applicable license, the applicable license prevails.
4. A HIT label does not determine copyrightability. Whether rights arise in parts generated by AI depends on the laws of each jurisdiction. A license applies to the extent that rights exist.
5. The declarant SHOULD state the license that applies to the disclosed materials.

### 10.2 Creative Commons

1. A HIT label is not part of the attribution (credit) requirements of CC licenses. It is written alongside the text that satisfies the attribution requirements.
2. A person who distributes an adapted work under ShareAlike (SA) terms SHOULD update the label in accordance with 8.4. However, updating the label is not a condition of the CC license.

### 10.3 Open-Source Licenses (GPL, MIT, Apache 2.0, etc.)

1. In source files, the label is written as a comment near the license notice (such as `SPDX-License-Identifier`). `HIT:` is not an official SPDX field and is treated as an independent comment line.

   ```text
   // SPDX-License-Identifier: Apache-2.0
   // HIT: HIT-A2-PT
   // AI: <provider> <model>  Created: 2026-11-15
   ```

2. A label for the entire repository MAY be written in the README or in a dedicated file.
3. If a HIT label is written in the NOTICE file under the Apache License 2.0, redistributors must retain the contents of the NOTICE file (Section 4(d) of that license). The declarant SHOULD choose where to write the label with this effect in mind.

### 10.4 Source-Available Works

1. The display method follows 10.3.
2. Disclosure of prompts or source code does not grant any right of use beyond what the applicable license permits.

### 10.5 Works Involving Transfer of Rights (Commissioned Production, Commissioned Development, etc.)

1. A HIT label is attached to the deliverables, and the disclosed materials are attached when the contract requires it. The disclosed materials MAY include records of the generation process at the level of differences (diffs).
2. Responsibility and warranties regarding the accuracy of the label are defined by the contract. This specification places no restrictions on the content of contracts.

### 10.6 Provision under a Non-Disclosure Agreement

1. Provision of the disclosed materials MAY be limited to the parties to the contract (6.3).
2. A HIT label MAY be used as a means of declaring compliance with internal rules or compliance requirements.

---

## 11. Internationalization

1. The identifier `HIT` and the flags MUST be written only with the letters defined in this specification. A label in which flags are replaced with characters of other languages (a localized label) does not conform to this specification.
2. When the target content or this specification is translated, the HIT label is not translated and is written as it is.
3. Normative language is translated according to the correspondence table in 2.2.
4. Interpretations for each jurisdiction (copyrightability, treatment of AI-generated works, and so on) are handled by jurisdiction profiles. Profiles MUST NOT change the core vocabulary.

---

## 12. Declaration Levels

| Level | Name | Content | Treatment in this document |
| --- | --- | --- | --- |
| L0 | Label | The HIT label is shown within the content. | Specified in this document. |
| L1 | Structured | Machine-readable metadata is embedded, or provided as a sidecar (such as JSON-LD). | To be specified in a separate document. |
| L2 | Verifiable | A signature such as C2PA is attached. Third parties can confirm the declarant and whether the content has been altered. | To be specified in a separate document. |

A higher level includes the lower levels. Even for declarations at L1 or above, the L0 label SHOULD be displayed.

---

## Appendix A: Disclosed Materials for This Document

| Flag | Content | Location |
| --- | --- | --- |
| `S` | The system prompt set by the declarant. Non-public parts set by the platform operator are not included. | [prompts](./archives/prompts/) |
| `P` | The full text of the prompts used to create and translate this document, and of the AI's responses | [prompts](./archives/prompts/) |
| `O` | The Japanese original of this document, and the original draft of the specification. The AI-generated content before editing can be traced through the repository's commit history. | [Japanese original](./HIT-L0-spec-v0.1.1.md), [HIT-base-doc-v0.0.1.md](https://github.com/hit-annotation/docs/blob/v0.1.0/HIT-base-doc-v0.0.1.md) |
| `R` | List of references | Appendix B |
| `T` | Created: 2026-11-15. Editing dates and times are recorded in the repository's commit history. | Label table at the beginning of this document |

---

## Appendix B: References

1. [Draft "Human Indication and Traceability (HIT) Annotation Overview" (provided to the AI when this document was generated)](https://github.com/hit-annotation/docs/blob/v0.1.0/HIT-base-doc-v0.0.1.md)
2. IPTC, Digital Source Type vocabulary: <https://cv.iptc.org/newscodes/digitalsourcetype/>
3. Creative Commons, Attribution 4.0 International Legal Code: <https://creativecommons.org/licenses/by/4.0/legalcode>
4. RFC 2119, Key words for use in RFCs to Indicate Requirement Levels: <https://www.rfc-editor.org/rfc/rfc2119>
5. SPDX Specification: <https://spdx.dev/>
6. Apache License, Version 2.0: <https://www.apache.org/licenses/LICENSE-2.0>
7. C2PA (Coalition for Content Provenance and Authenticity): <https://c2pa.org/>
8. ISO 8601, Date and time format: <https://www.iso.org/iso-8601-date-and-time-format.html>
