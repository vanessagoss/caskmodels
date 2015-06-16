### Original Cask Info
* The cask system is the NAC International UMS System. Please see [Images](../gh-pages/Images/) for images of the geometry. The original cask input is a SCALE 6.2 (beta) input generated by the Template Engine and 
is a model of the UMS Universal Transport Cask. This is a cask designed to hold and protect the cannister and environment during transport, 
i.e. rail transport. The cannister modeled is named the TSC-1 cannister. This is a cannister designed to hold PWR fuel assemblies.
The Transport Cask was modeled using dimensions that correspond to the TSC-1 cannister.
* The TSC-1 can hold 24 PWR fuel assemblies. The fuel composition and the source used in the input corresponds to a given loading map presented in
the table below. The material composition of the fuel is a fresh UO2 composition.  The source terms were generated using the ORIGAMI code. This generates binary source files for each of the assemblies which are imported
by the SCALE input. All source terms are decayed to May 6th, 2015.

| Position | Assembly_id | Burnup (MWd/MTU) | Enrichment | Discharge Date |
| :------: | :---------: | :--------------: | :--------: | :------------: |
|     1    |    B003     |       12276      |    2.41    |    6/29/1974   |
|     2    |    A065     |       11069      |    2.04    |    6/29/1974   |
|     3    |    EF0085     |       30391      |    2.52    |    1/11/1980  |
|     4    |    N858     |       37328      |    3.3    |    4/7/1990   |
|     5    |    J863     |       36802      |    3      |    3/31/1984   |
|     6    |    EF006L     |       30360      |    2.51    |    1/11/1980   |
|     7    |    C305     |       14884      |    2.95    |    5/2/1975   |
|     8    |    K042     |       35150      |    3    |    8/17/1985   |
|     9    |    P028     |       44137      |    3.5    |    2/14/1992   |
|     10    |    M857     |       43923      |    3.3    |    10/15/1988   |
|     11    |    M416     |       36781      |    3.3    |    10/15/1988   |
|     12    |    B050     |       16135      |    2.4    |    5/2/1975   |
|     13    |    EF005R     |       18367      |    1.94    |    4/9/1977   |
|     14    |    Q442     |       34250      |    3.69    |    2/14/1992   |
|     15    |    LT71     |       41988      |    3.29    |    3/28/1987   |
|     16    |    N416     |       42063      |    3.3    |    4/7/1990   |
|     17    |    K015     |       37796      |    3    |    8/17/1985   |
|     18    |    C234     |       13778      |    2.96    |    5/2/1975   |
|     19    |    EF0089     |       30200      |    2.52    |    1/11/1980   |
|     20    |    H208     |       36126      |    3.03    |    9/24/1982   |
|     21    |    M435     |       38956      |    3.3    |    10/15/1988   |
|     22    |    EF006V     |       30200      |    2.52    |    1/11/1980   |
|     23    |    C215     |       16525      |    2.94    |    5/2/1975   |
|     24    |    B017     |       12159      |    2.4    |    6/29/1974   |


***

### Storage Cask
* The original transfer cask input was modified to create a dry storage cask input. The dry storage cask modeled is the NAC International UMS Universal Storage System Vertical Concrete Cask (VCC).
This dry cask was chosen because it is compatible with the TSC-1 cannister and is part of the same fuel storage system by NAC International. The VCC is typically used for dry storage of spent fuel in ISFSIs.
* The information used to model the VCC was obtained from Safety Analysis Reports (SAR) submitted by the manufacturer to the NRC. These were found using the NRC ADAMS system. More information can be found 
in [Notes](./Notes.md).


***

### Input Modification
* The original transfer cask input is created by the Template Engine and is generated from multiple sub-templates. The sub-templates include SCALE input for cask geometry, source terms, arrays, and material
compositions. The main modifications were to create a new sub-template for the VCC geometry and to modify the existing material composition sub-template.

**Geometry Modification**
* The input geometry is built up semi-recursively (think Russian Dolls). There are separate sub-templates for fuel pins, which go into the fuel assemblies, which are repeated and go into the TSC-1 cannister, which
is then ultimately placed inside the transfer cask overpack. Because the VCC is compatible with the TSC-1 cannister contained in the original transfer cask input, and the already modeled fuel assemblies are acceptable,
the only modification required was to create a new sub-template for the VCC overpack. 
* Currently the type of overpack to use in the model when using the Template Engine is determined by the "analysis_type" key in the .json parameters file. The VCC will be generated by the Template Engine by using "VCC"
 as the analysis_type value. The "VCC" will instruct the Template Engine to insert the VCC sub-template as the overpack geometry when constructing the SCALE input. The TSC-1 cannister and everything else inside remained
 the same as the original transfer cask model.

**Main Features of the VCC Cask*
* The VCC overpack is primarily made of concrete 28 inches thick, with an inner steel liner 2.5 inches thick. At the bottom of the cask is a steel structure called the base weldment. This acts as both a support for the cannister
 and a structure that directs air from the air inlets. 4 air inlets are connected to the base weldment and protrude through the concrete overpack to pass air from outside to inside the cask, to pass upwards through the annulus of air
 formed between the cannister and the cask. At the top of the cask are 4 air outlet passages. These are offset 45 degrees from the air inlets at the bottom of the cask. The air outlets are a labyrinth, steel-lined passage that allows
 air to pass from inside the cask to the outside, while minimizing radiation streaming. The top of the cask has a 2 inch thick steel lid. Sandwiched beneath the lid and above the TSC-1 cannister is the shield plug. This is a 5 inch thick
 cylindrical plug made of carbon steel and neutron absorbing material. The shield plug sits on top of a support ring on the inner diameter of the steel liner, just above the TSC-1 cannister top.
