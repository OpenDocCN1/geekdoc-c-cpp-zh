
# Personalized Configuration

Juha Tiihonen*, Alexander Felfernig† and Monika Mandl†
*Aalto University, Aalto, Finland
†Graz University of Technology, Graz, Austria

Abstract: The increasing size and complexity of products (or product assortments) triggers a demand for intelligent techniques that proactively support users of configurator applications in finding a solution (configuration) that fits their wishes and needs. Recommendation technologies are predestined to be applied in the configuration context, because they can find relevant items from large and complex item sets. In this chapter, we show how different types of basic recommendation technologies can be applied to recommend configurations or individual selections such as attribute values to the user of a configurator. This discussion is based on a working example from the domain of mobile phones.

## 13.1 Introduction

Configuration systems (configurators for short; Barker et al., 1989; Heiskala et al., 2007; Stumptner, 1997) have become an important instrument to implement the concepts of mass customization (see Piller and Blazek, 2014¹). The basic concept of mass customization is the production of customer-individual products with near Mass Production efficiency (Pine, 1993; Tseng and Jiao, 2001). Following the paradigm of mass customization, the intelligent customizing of products and services is crucial for manufacturing companies to stay competitive. Configurators support the idea of integrating the user in the design process by allowing the specification (design) of desired product features; subsequent production processes take into account this individualized design. Instead of choosing a product, a user of a configurator specifies a product by configuring the product attributes based on a set of available options. Example domains where configurators are applied are computers, cars, industrial machinery, financial services, and telecommunication switches.

Configurators have many advantages such as the elimination of errors, shorter product delivery cycles, and increased productivity of sales representatives (see Bagley et al., 2014²). A major drawback of product configurators is that users (customers) in many cases have the problem of not fully understanding the set of offered options and are often overwhelmed by the complexity of these options (Bettman et al., 1998; Huffman and Kahn, 1998). The purpose of this chapter is to present a selected set of strategies to support users throughout the configuration process by integrating (exploiting)

¹Chapter 9.
²Chapter 4.

assignments in I are consistent with the constraints in C. A configuration is *complete* if all the variables in V have a concrete value, and, finally, a configuration is *valid* if it is both consistent and complete.

An example of a valid configuration is the following: `{styleReq=clam, webUse=often, GPSReq=false, pModel= p3, pStyle=clam, pHSDPA=3.6, pGPS =false, pPrice=99}`.

## 13.3 Integrating Recommendation Technologies to Configurators

A side effect of the high diversity of products that can be specified with a configurator is that the complexity of the offering may outstrip a user’s capability to explore the solution space and to make a buying decision. Previous research shows that consumers are often overwhelmed by the large amount of options (Malhotra, 1982). Since humans have limited processing capacity, confronting consumers with too much information can lead to an information overload and, therefore, can result in decreased quality of decision performance (Jacoby et al., 1974). Another challenge is that users often have no clear knowledge of what solution might fulfill their needs (Bettman et al., 1998). The *theory of preference construction* (Bettman et al.) explains that users typically do not know exactly which products or components they like (see also Mandl et al., 2014). As a consequence, users construct and adapt their preferences within the scope of a configuration process (Bettman et al., 1998).

Recommendation technologies can support users in the specification of their requirements and thus can help to achieve a higher user satisfaction (Cöster et al., 2002; Helferning et al., 2010; Geneste and Ruet, 2001). The integration of recommendation technologies with knowledge-based configuration is still in a very early stage. There exist some contributions that take into account the application of personalization technologies in the configuration context. Geneste and Ruet (2001) introduce an approach to the integration of case-based reasoning methods (Kolodner, 1993; McSherry, 2003) with constraint solving (Tsang, 1993; Mackworth, 1977). Cöster et al. (2002), Tihonen and Helferning (2010), and Helferning et al. (2010) focus on the recommendation of features, feature values, and strategies to integrate these recommendations in the user interface.

Next, we will discuss selected approaches to support users interacting with a configuration environment by the application of recommendation technologies.

### 13.3.1 Default Recommendations

In the remainder of this chapter, *defaults* refer to preselected feature values that represent recommended, meaningful alternatives that are compatible with the current user preferences. Defaults support the idea that users specify only those features which are important for them and let the system automatically determine values for the remaining ones (Falkner et al., 2011). Different approaches for recommending defaults are presented in the following paragraphs.

**Static default recommendation.** One interpretation of a static default is that a parameter has a predefined value that is independent of the configuration context. An alternative concept of static defaults has been introduced by McSherry (2005), who determines static recommendations for items based on the idea that most users would like to maximize or minimize values of numeric product attributes. These attributes are denoted as *more-is-better* (MIB; e.g., resolution or optical zoom of digital cameras) or

*less-is-better* (LIB; e.g., price or weight) attributes. Furthermore, for some attributes users prefer a high similarity between their preferences and the corresponding product attributes. An example of such a *nearer-is-better* (NIB) attribute is *pGPS*: if the user expects the availability of GPS, the configuration should include this feature. A *default query* specifies the optimal product; it consists of the following preferences: the maximum values for MIB attributes, the minimum values for LIB attributes, and the user requirements for NIB attributes.

For our mobile phones example (Table 13.1) the preferred value for the LIB attribute `pPrice` is 69 (price of the cheapest available phone). The preferred value for `pHSDPA` is 7.2 (MIB; the highest available data rate). Finally, the preferred value for NIB attribute `pGPS` is *true* assuming that the customer (user) requires GPS (*GPSReq = true*). The resulting default query is *Q = {pPrice = 69; pHSDPA = 7.2; pGPS = true}*.

The similarity of item *I* to the default query *Q* is determined with respect to each attribute *a* in *Q*. Formula 13.1 is used for MIB attributes, Formula 13.2 for LIB attributes, and Formula 13.3 for NIB attributes (McSherry, 2005). In these formulae, *max(a)* and *min(a)* refer to the maximum and minimum values of the attribute *a* in the case base. *φₐ(Q)* is the value of *a* in the (default) query *Q* and *φₐ(I)* is the value of *a* for the item *I*. In these formulae, Boolean attributes values *false* and *true* are interpreted as 0 and 1, respectively. The union of all attributes in the case base is *V* (the set of variables).

sim_(MIB)(a, I, Q) = 1 - |φₐ(I) - φₐ(Q)| / [max(a) - min(a)] = [φₐ(I) - min(a)] / [max(a) - min(a)]   (13.1)

sim_(LIB)(a, I, Q) = 1 - |φₐ(I) - φₐ(Q)| / [max(a) - min(a)] = [max(a) - φₐ(I)] / [max(a) - min(a)]   (13.2)

sim_(NIB)(a, I, Q) = 1 - |φₐ(I) - φₐ(Q)| / [max(a) - min(a)]   (13.3)

Applying static default recommendation to the phones in Table 13.1 for the query *Q = {pPrice = 69; pHSDPA = 7.2; pGPS = true}*, we calculate the similarities for the numeric attributes `pPrice`, `pHSDPA`, and `pGPS` (see Table 13.2).

Table 13.2 Static default recommendation for phone models of the working example. `pModel` is the phone model, `pHSDPA` is the supported HSDPA data rate, and `sim_pHSDPA` is similarity value of the MIB attribute `pHSDPA` (Formula 13.1). `pPrice` is the price of the phone, `sim_pPrice` is the similarity value of the LIB attribute `pPrice` (Formula 13.2). `pGPS` specifies if the phone supports GPS, and `sim_pGPS` is the similarity value of the Boolean NIB attribute `pGPS` (Formula 13.3). Finally Σ represents Σₐ∈V sim(a, pModel, Q)—the total similarity of pModel with regard to best values Q.

| pModel | pHSDPA | sim_pHSDPA | pPrice | sim_pPrice | pGPS | sim_pGPS | Σ |
|---|---|---|---|---|---|---|---|
| p1 | 0 | 0.000 | 69 | 1.000 | false | 0.000 | 1.000 |
| p2 | 7.2 | 1.000 | 149 | 0.000 | true | 1.000 | 2.000 |
| p3 | 3.6 | 0.500 | 99 | 0.625 | false | 0.000 | 1.125 |
