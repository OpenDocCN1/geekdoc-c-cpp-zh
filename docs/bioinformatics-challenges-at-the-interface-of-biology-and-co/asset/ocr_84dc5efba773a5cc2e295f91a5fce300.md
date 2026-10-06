# Bioinformatics challenges at the interface of biology and computer science

LSID system, although it still enjoys in zoological and taxonom areas of biology, where LSIDs are used to identify taxonomic names (se Page, 2006).

# DOIs

In early 2000, a group of academic publishers came together to form Crossref, an independent organisation with a mission,

+   to enable easy identification and use of trustworthy content by promoting the cooperative development and application of a sustainable infrastructure.

As a 'trusted' DOI Registration Agency, Crossref enabled the use of a consistent, electronically resolvable identification scheme across all manner of academic disciplines. Bringing together a critical mass of competing publishers to cooperate on a competitive task – one of such valuable to all concerned – was a gargantuan task, requiring deft political maneuvering. The process nearly found many times; however, the benefit of the DOI applied to scientific literature has numerous.
A Digital Object (DOI) is a qualified identifier used to reference some digital object in a way that's independent of its location on the Web. DOIs are primarily used to identify identical resources (articles or parts of) for use in citations and cross-references, but can theoretically be used to identify any locatable resource.
The pure form of the DOI, and an example,

```
doi: <RI><RT>/<ID>
doi: 10.1042/BJ20091474
```

Here, after initial doi: we see three levels of identification, beginning with the 10, which identifies the DOI registry (RI), continuing with the number 1042, which identifies the DOI registrant (RT), and finally, the string BJ20091474 (ID), which uniquely identifies an object within that registrant's namespace. This example refers to an article registered by the publisher Portland Press Ltd. with the Crossref registry.
Because pure DOIs are indistinguishable URIs, there needs be a central registry and resolution service to map them to locations on the Web. The International DOI Foundation provides such a service, taking a DOI and returning a URI.

```
http://www.biochemj.org/bj/424/bj4240317.htm
```

As a convenience, Crossref provides a dereferencing service that allows DOIs for articles registered with them to be written in the form:

```
http://dx.doi.org/10.1042/BJ20091474
```

which resolves to the same problem for URI in the biochem.org domain.
As mentioned previously, this DOI could change at any point, if the journal's website was registered, but the DOI will remain the same; so whereas linking to biochem.org directly easily break in the future, taking the small cost of extra step of dereferencing via Crossref, or the International DOI Foundation, provides an additional level of robustness against change.

Unfortunately, versioning and provenance are absent from the DOI system, so we need to be confronted with the same problems in literature as we are with biological databases. A single DOI often refers to the latest version of an article, no explicit