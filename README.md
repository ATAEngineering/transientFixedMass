# Transient Fixed Mass Module
This module was developed by [ATA Engineering](http://www.ata-e.com) as an 
add-on to the Loci/CHEM computational fluid dynamics (CFD) solver. The 
module can be used to extend Loci/CHEM's `fixedMass` boundary condition to
accept time varying data.

# Dependencies
This module depends on both Loci and CHEM being installed. Loci is an open
source framework developed at Mississippi State University (MSU) by Dr. Ed 
Luke. The framework provides a rule-based programming model and can take 
advantage of massively parallel high performance computing systems. CHEM is 
a full featured open source CFD code with finite-rate chemistry built on 
the Loci framework. CHEM is export controlled under the International 
Traffic In Arms Regulations (ITAR). Both Loci and CHEM can be obtained from 
the [SimSys Software Forum](http://www.simcenter.msstate.edu) hosted by 
MSU. This module also requires a compiler with C++11 support.

# Installation Instructions
First Loci and CHEM should be installed. The **LOCI_BASE** environment
variable should be set to point to the Loci installation directory. The 
**CHEM_BASE** environment variable should be set to point to the CHEM 
installation directory. The installation process follows the standard 
make, make install procedure.

```bash
make
make install
```

# Usage
First the module must be loaded at the top of the **vars** file. 
The **fixedMass** boundary condition may be tagged with either 
**transientMassFlux** or **transientMdot** to specify a file containing the
time varying boundary condition data.

```
loadModule: transientFixedMass

boundary_conditions: <BC_1=fixedMass(transientMassFlux="massFlux.dat"),
                      BC_2=fixedMass(transientMdot="mdot.dat")>
```

The format of the specified file should be the following, where the mass 
quantity will be either the mass flux or mass flow rate depending on whether
**transientMassFlux** or **transientMdot** is specified. The file should use
SI units for all quantities.

```
number_of_species
species_name_1 species_name_2 ... species_name_n
number_of_time_points
time_1 mass_quantity_1 T0_1 mass_fraction_1_1 mass_fraction_1_2 ... mass_fraction_1_n
time_2 mass_quantity_2 T0_2 mass_fraction_2_1 mass_fraction_2_2 ... mass_fraction_2_n
...
time_m mass_quantity_m T0_m mass_fraction_m_1 mass_fraction_m_2 ... mass_fraction_m_n
```
