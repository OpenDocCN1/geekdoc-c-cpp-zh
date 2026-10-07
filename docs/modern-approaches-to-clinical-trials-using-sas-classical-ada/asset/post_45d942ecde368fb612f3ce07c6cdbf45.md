
# Modern Approaches to Clinical Trials Using SAS®

Classical, Adaptive, and Bayesian Methods

Edited by Sandeep M. Menon Richard C. Zink

The correct bibliographic citation for this manual is as follows: SAS Institute Inc. 2015. Modern Approaches to Clinical Trials Using SAS®: Classical, Adaptive, and Bayesian Methods Cary, NC: SAS Institute Inc.

Modern Approaches to Clinical Trials Using SAS®: Classical, Adaptive, and Bayesian Methods

Copyright © 2015, SAS Institute Inc., Cary, NC, USA

ISBN 978-1-62959-385-2 (Hardcopy)
ISBN 978-1-62960-082-6 (Epub)
ISBN 978-1-62960-083-3 (Mobi) 
ISBN 978-1-62960-084-0 (PDF)

All rights reserved. Produced in the United States of America.

For a hard-copy book: No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or by any means, electronic, mechanical, photocopying, or otherwise, without the prior written permission of the publisher, SAS Institute Inc.

For a web download or e-book: Your use of this publication shall be governed by the terms established by the vendor at the time you acquire this publication.

The scanning, uploading, and distribution of this book via the Internet or any other means without the permission of the publisher is illegal and punishable by law. Please purchase only authorized electronic editions and do not participate in or encourage piracy of copyrighted materials. Your support of others' rights is appreciated.

U.S. Government License Rights; Restricted Rights: The Software and its documentation is commercial computer software developed at private expense and is provided with RESTRICTED RIGHTS to the United States Government. Use, duplication or disclosure of the Software by the United States Government is subject to the license terms of this Agreement pursuant to, as applicable, FAR 12.212, DFAR 227.7202-1(a), DFAR 227.7202-3(a) and DFAR 227.7202-4 and, to the extent required under U.S. federal law, the minimum restricted rights as set out in FAR 52.227-19 (DEC 2007). If FAR 52.227-19 is applicable, this provision serves as notice under clause (c) thereof and no other notice is required to be affixed to the Software or documentation. The Government's rights in Software and documentation shall be only set forth in this Agreement.

SAS Institute Inc., SAS Campus Drive, Cary, North Carolina 27513-2414.

December 2015

SAS® and all other SAS Institute Inc. product or service names are registered trademarks or trademarks of SAS Institute Inc. in the USA and other countries. ® indicates USA registration.

Other brand and product names are trademarks of their respective companies.

# Foreword

Recent years, and perhaps particularly the past decade, have seen a rapid evolution in the statistical methodology available to be used in clinical trials, from both technical and implementation standpoints. Certain practices as they might have been performed not too far into the past in fact now somewhat primitive or naïve. Much, but by no means all, of the recent development is related to recent interest in adaptive trial designs. The term itself is quite broad, and encompasses a wide variety of techniques and applications. Many trial aspects are potential candidates for adaptation, including but not limited to: sample size or information requirements, dose or treatment regimen selection, targeted patient population selection, randomization allocation scheme; and within each of these categories there may be multiple and fundamentally different technical and strategic approaches that are now available for practitioners to consider.

Classical procedures as well have undergone advancements in the statistical details of their implementation, and their usage in analysis and interpretation of trial results. Enhancements in classical approaches, and the progress made or envisioned in utilization of novel adaptive and Bayesian designs and methodologies, are reflective of the current interest in the transition to personalized medicine approaches, by which optimal therapies corresponding to particular patient characteristics are sought. A categorization of designs and methods into classical, adaptive, and Bayesian methods is by no means mutually exclusive, as a number of methodologies have aspects of more than one of these classes. Just to cite one example, group sequential designs are a familiar feature in current clinical trial practice that fall under the classical and adaptive headings; this is also certainly an area that has seen an evolution in recent years. Aspects of clinical trial or program design such as dose finding or population enrichment may contain aspects that are adaptive, or Bayesian, or both, as is communicated in this volume.

The interest in novel adaptive and Bayesian approaches certainly does not preclude the possibility that classical approaches will be preferred in many situations; they maintain the attributes which led to their widespread adoption in the first place. As has been pointed out by many authors, the best use of these novel approaches will be realized by a full understanding of their behavior and an objective evaluation of their advantages and relevant tradeoffs in particular situations. This point is clearly and objectively conveyed throughout this volume, as approaches of varied types are presented not to promote or endorse their casual routine use, but rather are described with sufficient explanations to help practitioners make the best choices for their situations, and of course to have the computational tools to implement them.

It seems inevitable that the availability to users of software and computational capabilities is inextricably linked with increased consideration of and interest in alternative design and analysis strategies, and ultimately their implementation. Certainly, if a novel methodology is seen as adding value in such an important arena as clinical trials, it will spur development of the computational tools necessary to implement it. However, in a cycle, the increased availability to practitioners leads to increased consideration and implementation, which spurs further interest, enables learning from experience, perhaps motivates further research, and ultimately leads to further methodological and in-practice improvements and evolution.

Just as a simple illustration of this phenomenon: questions regarding how clinical sites should be accounted for in main statistical analysis models have undergone some debate in past decades, with occasional flurries of literature activity, but evolution in conventional practices was limited. The introduction of SAS MIX in the early 1990s provided a platform for more widespread consideration and usage of some approaches that were less utilized at that time, which incorporated clinical size as a random effect in analysis models in various manners. There were implications for important issues, such as sample size determination and targeted center-size distributions, and for certain practices that were in use at the time as small center pooling algorithms. Given the presence of the new computational tool available to users in the form of the SAS, it may not be a coincidence that by the latter part of that decade there was vigorous dialogue taking place in the literature on matters involving how best to design multicenter size and accommodate center within a relatively short period of time there were notable changes in conventional practices.

Given the extent of recent methodological advances, and the wide knowledge of and usage of SAS throughout the clinical trials community, a focused volume such as one is particularly timely in this regard. integrates a broad coherent summary of current approaches for clinical trial design and analysis, with particular emphasis on important recently developed ones, along with specific illustrations of how they can be implemented and performed in SAS. In some cases this involves relatively straightforward calls to SAS procedures; in many others, sophisticated SAS macros developed by the authors are presented. Motivating examples are described, and SAS outputs corresponding to those examples are explained to help guide readers through the most accurate understandings and interpretations. This text might well function effectively as a technical resource on state-of-the-art clinical trials methodology even if it did not contain the SAS illustrations and explanations; and it could also fit within a useful niche if it focused solely on the SAS illustrations without the methodological and practical explanations.

Paul Gallo

Novartis

October 2015
