
![](img/8bd670d4939cf71dbd0c6123d1b834ff_0_0.png)

## TOM CANAVAN

# CMS SECURITY HANDBOOK

### THE COMPREHENSIVE GUIDE FOR WORDPRESS®, JOOMLA!®, DRUPAL®, AND PLONE

DISCARDED

# CMS Security Handbook

### The Comprehensive Guide for WordPress®, Joomla!®, Drupal™, and Plone®

Tom Canavan

East Meadow Public Library  
1886 Front Street, East Meadow, NY 11554  
(516) 794-2570  
www.eastmeadow.info

![](img/8bd670d4939cf71dbd0c6123d1b834ff_2_0.png)

Wiley Publishing, Inc.

Copyright © 2011 by Wiley Publishing, Inc., Indianapolis, Indiana  
Published simultaneously in Canada

- ISBN: 978-0-470-91621-6
- ISBN: 978-1-118-09174-6 (ebk)
- ISBN: 978-1-118-09175-3 (ebk)
- ISBN: 978-1-118-09176-0 (ebk)

Manufactured in the United States of America

1 0 9 8 7 6 5 4 3 2 1

No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning or otherwise, except as permitted under Sections 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the appropriate per-copy fee to the Copyright Clearance Center, 222 Rosewood Drive, Danvers, MA 01923, (978) 750-8400, fax (978) 646-8600. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748-6011, fax (201) 748-6008, or online at http://www.wiley.com/go/permissions.

**Limit of Liability/Disclaimer of Warranty:** The publisher and the author make no representations or warranties with respect to the accuracy or completeness of the contents of this work and specifically disclaim all warranties, including without limitation warranties of fitness for a particular purpose. No warranty may be created or extended by sales or promotional materials. The advice and strategies contained herein may not be suitable for every situation. This work is sold with the understanding that the publisher is not engaged in rendering legal, accounting, or other professional services. If professional assistance is required, the services of a competent professional person should be sought. Neither the publisher nor the author shall be liable for damages arising herefrom. The fact that an organization or Web site is referred to in this work as a citation and/or a potential source of further information does not mean that the author or the publisher endorses the information the organization or website may provide or recommendations it may make. Further, readers should be aware that Internet websites listed in this work may have changed or disappeared between when this work was written and when it is read.

For general information on our other products and services please contact our Customer Care Department within the United States at (877) 762-2974, outside the United States at (317) 572-3993 or fax (317) 572-4002.

Wiley also publishes its books in a variety of electronic formats. Some content that appears in print may not be available in electronic books.

**Library of Congress Control Number:** 2011922796

**Trademarks:** Wiley and the Wiley logo are trademarks or registered trademarks of John Wiley & Sons, Inc. and/or its affiliates, in the United States and other countries, and may not be used without written permission. All other trademarks are the property of their respective owners. Wiley Publishing, Inc. is not associated with any product or vendor mentioned in this book.

*This book is dedicated to my wife, Carol Ann. Thank you for your support and love. You are more appreciated than I can likely ever tell you.*

*And I dedicate this book to you, dear reader, that in it you may find support in these trying cyber-security times.*

## Credits

- **Executive Editor**<br>Carol Long
- **Project Editor**<br>Kevin Shafer
- **Technical Editor**<br>David A. Chapa
- **Production Editor**<br>Kathleen Wisor
- **Copy Editor**<br>Paula Lowell
- **Editorial Director**<br>Robyn B. Siesky
- **Editorial Manager**<br>Mary Beth Wakefield
- **Freelancer Editorial Manager**<br>Rosemarie Graham
- **Marketing Manager**<br>Ashley Zurcher
- **Production Manager**<br>Tim Tate
- **Vice President and Executive Group Publisher**<br>Richard Swadley
- **Vice President and Executive Publisher**<br>Barry Pruett
- **Associate Publisher**<br>Jim Minatel
- **Project Coordinator, Cover**<br>Katie Crocker
- **Proofreader**<br>Jen Larsen, Word One New York
- **Indexer**<br>Robert Swanson
- **Cover Designer**<br>Ryan Sneed
- **Cover Image**<br>© Fuse / GettyImages

## About the Author

Tom Canavan has enjoyed an extremely successful career in the technology sector for more than 24 years, working for companies such as Dell Computer and Texas Instruments. He has served in the roles of Director of IT, CIO, and many other valued and highly sought-after positions throughout his career. Having worked at all levels from field technician to senior management, he brings distilled knowledge and wisdom from the enterprise level down to the small and medium business world. Canavan has a degree in Robotics and Computer Numerical Control. His background includes many years in the computer hardware industry, and extensive experience in data center operations and the information security sector. Canavan has authored several books, and is a frequent public speaker on the topic of IT/information security. He is co-founder of Salusvalerting.com.

## About the Technical Editor

David A. Chapa is a Senior Analyst with the Enterprise Strategy Group, a research and strategic consulting firm. He has invested more than 25 years in the computer industry, focusing specifically on data protection, data disaster recovery, and business resumption practices. He has held several senior-level technical positions with companies such as Cheyenne Software, OpenVision, ADIC, Quantum, and NetApp. He has been a featured speaker at a variety of industry events covering various topics related to disaster recovery, compliance, and the use of disk, tape, and cloud for recovery and backup strategies. He is recognized worldwide as an authority on the subject of backup and recovery. Chapa is also a member of SNIA's Data Protection and Capacity Optimization (DPCO) Committee, whose mission is to foster the growth and success of the storage market in the areas of data protection and capacity optimization technologies.

## Acknowledgments

For those who have never written a book, you never see the cast of many behind the author. While the writing belongs to the author, the quality of the writing is often enhanced by the team of people behind the author that make him or her look good. In my case, I believe I’m a decent writer, but with the editorial staff of Wiley, I look like a great writer. That “greatness” comes through the hard work and skill of the editors I had the honor to work with.

I wish to thank my Project Editor, Kevin Shafer, and his team for helping me to produce what I hope to be a truly great work. I wish to thank Carol Long, my Executive Editor, for putting up with multiple delays, and for the opportunity to put my experience on paper and bring it to you. I especially would like to thank the Technical Editor, David Chapa, for his most excellent and challenging technical peer review of this work.

Thanks to Jeff Star of perishablespress.com for his help with the art of .htaccess, and Doug Vann of dougvann.com for his valuable assistance with Drupal questions.

Special thanks to my good friend Mark Turner of Walt-Disney Corporation, who inspired the original idea for this work some time ago.

I thank my beautiful wife, Carol Ann, who has endured me writing yet another book and putting up with an unfinished remodel of our home during this time.

In my 20-plus years in the technology industry, I have met and learned from so many people that I cannot begin to recall them all. Please know you are not forgotten. I appreciate your wisdom and guidance.

And I wish to acknowledge and thank my Lord and Savior, Jesus Christ, who gave me the wisdom in this book and the ability to write it. Without Him I would not have ever embarked on this effort.

Lastly, I wish to thank you, dear reader, for purchasing this book and reading it. I truly hope that you will find answers to questions about your security that will keep you safe and operational.
