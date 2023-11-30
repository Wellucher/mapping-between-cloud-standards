# Data Preprocessing

## 1 Original Data Collection

In order to build the required data set, we selected some cloud security standards and extracted their control item texts from the corresponding official websites. The text formats published by different cloud security standards are different, including **xlsx, csv, xml, pdf, html**, etc.

 Below we list the links and corresponding file formats to the text files of the cloud security standard control items we involve. (If there are any errors or omissions, please contact us)

|                   Cloud Security Standard                    |                       Official Website                       | File Format |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :---------: |
|                         CSA CCM V3.0                         | https://cloudsecurityalliance.org/artifacts/identity-and-access-management-glossary/ |    xlsx     |
|                        Canada PIPEDA                         | https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-personal-information-protection-and-electronic-documents-act-pipeda/p_principle/ 与 https://laws-lois.justice.gc.ca/eng/acts/p-8.6/page-7.html |    html     |
|                            COBIT5                            | https://www.scribd.com/document/444651729/3-COBIT-5-Self-assessment-Templates-xlsx |    xlsx     |
|                            COPPA                             | https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa |     xml     |
|                      CSA Guidance V3.0                       | https://cloudsecurityalliance.org/artifacts/security-guidance-for-critical-areas-of-focus-in-cloud-computing-v3/ |     pdf     |
|                          ENISA IAF                           | https://www.enisa.europa.eu/publications/cloud-computing-information-assurance-framework |     pdf     |
|     95/46/EC  - European Union Data Protection Directive     | https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:31995L0046 |    html     |
|                            FERPA                             |   https://www.ecfr.gov/current/title-34/subtitle-A/part-99   |     xml     |
|                            HIPAA                             | https://www.hhs.gov/hipaa/for-professionals/privacy/laws-regulations/combined-regulation-text/index.html |     xml     |
|                         HITRUST CSF                          |      https://hitrustalliance.net/csf-license-agreement/      |     pdf     |
|                      ISO/IEC 27001:2013                      |        http://www.itref.ir/uploads/editor/42890b.pdf         |     pdf     |
|                             ITAR                             | https://www.ecfr.gov/current/title-22/chapter-I/subchapter-Mhttps://www.ecfr.gov/current/title-15/subtitle-B/chapter-VII/subchapter-C |     xml     |
|                        Jericho Forum                         | https://static.spiceworks.com/attachments/post/0016/4842/commandments_v1.2.pdf |     pdf     |
| Mexico - Federal Law on Protection of Personal Data Held by Private Parties | https://www.global-regulation.com/translation/mexico/560242/federal-law-of-protection-of-personal-data-in-the-possession-of-private-individuals.html |    html     |
|                       NIST SP800-53 R3                       | https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/downloads |     csv     |
|                         PCI DSS 3.2                          | https://www.pcisecuritystandards.org/document_library/?category=pcidss&document=pci_dss |     pdf     |
|                              C5                              | https://www.bsi.bund.de/EN/Themen/Unternehmen-und-Organisationen/Informationen-und-Empfehlungen/Empfehlungen-nach-Angriffszielen/Cloud-Computing/Kriterienkatalog-C5/C5_AktuelleVersion/C5_AktuelleVersion_node.html |    xlsx     |
|                   NIST 800-53 R4 Moderate                    | https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/downloads |     csv     |
|                        AICPA TSC 2017                        | https://us.aicpa.org/content/dam/aicpa/interestareas/frc/assuranceadvisoryservices/downloadabledocuments/trust-services-criteria-2020.pdf |     pdf     |
|                     FedRAMP R4 Moderate                      |         https://www.fedramp.gov/documents-templates/         |    xlsx     |
|                             CIS                              | https://www.cisecurity.org/benchmark/amazon_web_services?sc_camp=F08237A092B040A590AA789FA2FB9C40&gclid=CjwKCAjwo9unBhBTEiwAipC111rLhM0-QLavhVst8bFO93KUM7DfG_OD5pNwTbzKLrXYoXANGorM-BoCBlkQAvD_BwE |     pdf     |

## 2.Text Preprocessing and Formatting

Considering that CSA Cloud Security Control Matrix (CSA CCM) is used as the main mapping reference standard in this work, in order to ensure the consistency of the text data format, we choose the index-control item text format of CSA CCM as the standard format. At the same time, we have adopted different processing methods for different formats of cloud security standard documents.

* For texts in **pdf** and **html** formats, we manually extract the control item IDs and corresponding texts of each cloud security standard;
* For text in **xml** format, we extract the control item ID and corresponding text by parsing the xml;
* For text in **csv** and **xlsx** format, just extract the corresponding index and control item text directly.

At the same time, because most of the cloud security standard texts selected in this work are in English, we uniformly translated non-English cloud security standard texts into English.

## 3.Indirect Mapping Generation

Considering that **CSA CCM v3.0** and **HITRUST CSF v8.1** already have mappings of control items with other cloud security standards, we selected these two cloud security mappings as the original mappings and obtained **4957** pieces of original mapping data in which containing a large number of many-to-many mappings.Then We then generate indirect mappings between other cloud security standards via the original mapping. 

Its specific generation rules are as follows:

 For cloud security standards S~1~,S~2~ ,S~3~, they each contain the cloud security standard text S~i~^j^ (S~i~^j^ ∈S~i~, i= 1,2,3, j=1,2,....), S~i1~^j1^ *↔* S~i2~^j2^ means that there is a mapping between the two control item texts.

 If S~1~^j1^ *↔* S~2~^j2^ and S~1~^j1^ *↔* S~3~^j3^ are original mappings, then we generate indirect mapping S~2~^j2^ *↔* S~3~^j3^.

Accordingly, we finally obtained the mapping relationship matrix between 21 standards, with **114,373** mapping data。
