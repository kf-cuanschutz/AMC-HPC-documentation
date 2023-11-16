# FAQ 
  =========================

### 1) When is the Preventative maintenance performed (PM)?

   CU Boulder performs preventative maintenance every first Wednesday of the month.

### 2) Where can I follow CU Boulder (PM) updates?

   PM updates can be followed [here](https://curc.statuspage.io/). There, you will know if Alpine is affected by the maintenance. 
   You can also subscribe to the page.

### 3) Will my Alpine jobs get killed because of the PM?

   It depends but usually jobs are held until after the maintenance.
   However, the screen sessions usually get killed if they were launched on the login node
   
### 4) How to install Globus personal as well as a persnal collection name?
   * The following tutorial explains steps as steps the procedure on Macbook [machines](https://docs.globus.org/how-to/globus-connect-personal-mac/)
   * The following tutorial addresses the issue on Windows [machines](https://docs.globus.org/how-to/globus-connect-personal-windows/)
   * Finally, the following tutorial addesses the issue on Linux [machines](https://docs.globus.org/how-to/globus-connect-personal-linux/)

### 5) How can I access Globus DTN23 collection?

  Please follow this [short guide](https://github.com/kf-cuanschutz/CU-Anschutz-HPC-documentation/blob/main/Workshops/globus_guide.pdf)

### 6) How can I share my folder on Alpine with someone from another institution?

   In order to achieve that one will have to create a guest collection. Make sure that the collaborator who wants to access your path has access to Globus.
   This methods works for /projects/$USER, /scratch/alpine/$USER, /pl/active/allocation_name or /pl/archive/allocation_name.
   Please follow the procedure [here](https://github.com/kf-cuanschutz/CU-Anschutz-HPC-documentation/blob/main/Globus-guest-collection-files/Presentation_Globus_guest_collection.pdf)
   in order to create guest collection on Alpine.
