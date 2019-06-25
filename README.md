# Unit-Commitment-AIMMS-Model
User Manual for AIMMS Unit Committemnt Power System Modelling
This manual allows the reader to follow the document from start to end
(continuous reading) or to find certain information as one would do in a
directory or in a reference text; hence the name *User Manual*. It has
been properly indexed at the end of the document to ease the process of
finding specific words or phrases in the text. Where necessary,
references to external sources or publications are also provided.

**Technologies**\

Non-dispatchable
:   ***Large Solar***; ***Onshore Wind***; ***Offshore Wind***; ***Small
    Solar** (Rooftop Solar PV)*

Baseload
:   ***Nuclear***\
    *Carbon Capture and Storage* (**CCS**)

    -   Post-combustion Carbon Capture

        -   Natural Gas Combined Cycle (**NGCC-PCC**)

            -   w/out Rich and Lean Amine Solvent Tank

    -   Oxy-combustion Capture

        -   Allam Cycle (**AC**)

            -   w/out Oxygen Storage Tank

Midload
:   *Combined Cycle Gas Turbine* (**CCGT**)

Peakload
:   *Open Cycle Gas Turbine* (**OCGT**)

Energy Storage
:   *Pump Hydro Storage* (**PHS**); *Compressed Air Energy Storage*
    (**CAES**); ***Flywheel***; ***Flow Battery***; ***Hydrogen Fuel
    Cell***

Demand Response
:   Price-responsive demand response from industrial complexes

Renewable Curtailment
:   Curtailment-prone ***Large Solar***, ***Onshore Wind***, ***Offshore
    Wind*** and ***Small Solar***

Load Shedding
:   Expensive curtailment of demand as a measure of the last resort

There are many Unit commitment (UC) models in the world and most of them
are extensively used for electricity system analyses @hobbs2006next.\
This manual is for models that use electricity systems with detailed
plant characteristics. The models presented are executed with mixed
integer programming (MIP) developed in AIMMS algebraic modelling
environment. All model versions assume continuous serving of electricity
demand in hourly increments where there is no start-up requirement at
the beginning of the first hour for the whole optimisation period. There
are no transmission constraints and the system is assumed to have one
central bus.\
The models can be tailored to solve for overall system cost
minimisation, for plant profit maximisation or even for bi-level
optimisation, *i.e.* when the objective is to reach an equilibrium state
for both system and plant operators.\

Downward reserve is excluded from the MIP model as multiple simulations
has shown that downward reserve requirement is always satisfied whenever
upwards reserve requirement is satisfied too.\

Naming of the model indicates what features are included in the model.
It is highly recommended to keep the latest version of the model which
has all necessary features and technologies included. Although there are
many technology choices in the model, one can choose any subset of
technologies and run the optimisation with these subsets. The modeller
can also choose to run the deterministic or stochastic version of the
same model; the model can be run even in a bi-level mode, as described
above.\
The developed models are versatile and one can use them to solve both
for short-term planning (*e.g.* weekly) or long-term planning (*e.g.*
yearly) horizons. For long-term planning problems, suggested models to
use are *daily*, *weekly* or *bi-weekly* decomposition options. Although
long-term operational planning problems are not often used in real-life
power system scheduling, they are valuable tools for research purposes
when long-term system outcomes, such as annual CO2 emissions or CO2
emission intensities for comparable studies are analysed.

Essentials {#Introduction}
==========

Author, Credits and Licence
---------------------------

This manual is intended for the users of [AIMMS UC
model](https://gist.github.com/vitali87/f38a7aa1b3e85b788b90811b1ee4d39c).
It provides information in a specific format to help the reader find the
right information easily.

The models are developed and the content is written by [Vitali
Avagyan](https://www.linkedin.com/in/vitali-avagyan-a1566234/), a
research associate at the Institute of Energy Systems, The University of
Edinburgh. The author thanks his line Manager, [Hannah
Chalmers](https://www.eng.ed.ac.uk/about/people/dr-hannah-chalmers), for
supporting him throughout the post-doctoral period and providing
assistance needed when producing this user manual.

When using models, please cite one of the papers co-authored by the
author to give kudos attached to the numerous hours spent on developing
these models. Much appreciated in advance!\
Citable papers are:

-   *Flexibility Revisited: The Role of Conventional Generators in the
    Future GB Electricity System*

-   *Highly flexible zero carbon electricity generation: An initial
    assessment of the value of Allam Cycle power plants with liquid
    oxygen storage in future GB electricity system*

Please, check for the final publication details when citing the papers
as currently they are being submitted or are under revision.

Academic AIMMS licences are given for a 6-month period and can be freely
renewed after expiration.

Changing the Model {#Changing}
------------------

If you want to change the existing model from the one(s) distributed to
you, the following steps should be undertaken:

1.  The model folder has to be copied in the same directory.

2.  The name of the model (folder) has to be altered. This change should
    preserve the convention used before (to the taste of the modeller).
    The author prefers the following format:

        PRofit_store4_MIP_pw_CCS_ES_RES_AC_xml

    which reads as “Profit-Store model, version 4, using mixed integer
    programming technique that includes energy storage, renewable energy
    sources and Allam-Cycle plants. Outputs are also produced in XML
    files.”

    The main purpose of a name layout is to make sure the modeller gives
    enough information for differentiating between model & feature
    releases.

    You can find detailed information about model features and options
    in chapter [optimisation~o~ptions].

3.  Name of the file that has *.aimms* extension inside the newly
    created folder should be changed to the folder name that contains
    it. In our case it will be:

        PRofit_store4_MIP_pw_CCS_ES_RES_AC_xml.aimms

4.  Name of the file that has *.ams* extension inside MainProject folder
    should be changed to the following:

        PRofit_store4_MIP_pw_CCS_ES_RES_AC_xml.ams

5.  Inside `MainProject` folder, Project*.xml* file should be opened
    (edited) with the help of Notepad or Notepad++. After changes, your
    file should look something like this:

        <?xml version="1.0"?>
        <Project AimmsVersion="4.59.4.1 unicode x64" ProjectUUID="E53615B9-A4D4-49B5-9E5A-0B9D088F7D1B">
          <ModelFileName>..\..\PRofit_store4_MIP_pw_CCS_ES_RES_AC_xml\MainProject\ProfitStore4_pw_CCS_ES_RES_AC_xml.ams</ModelFileName>
          <AutoSaveAndBackup>
            <DataBackup AtRegularInterval="true" EveryNMinutes="15" NumBackupsDatedToday="3" NumDaysBeforeToday="3" />
          </AutoSaveAndBackup>
        </Project>
         

    Where you make sure that row `<ModelFileName>` has been altered
    accordingly to adjust to the model file name. The file then should
    be saved and closed.\
    Not essential though, it is highly recommended to adjust the name of
    the *.nch* file to the model name too.

    Chapter [ams] contains more information about building/changing the
    entire model inside *.ams* file. In contrast, Chapter
    [optimisation~o~ptions] and Chapter [global~i~nput~p~arameters] are
    devoted to building/changing the model in the AIMMS Interactive User
    Interface (IDE). For more information about AIMMS IDE, refer to
    [AIMMS
    Developer](https://aimms.com/english/developers/product-info/aimms-developer/user-interface/)
    web page.

    Unfortunately, the modeller needs a Windows PC to develop a model
    for academic purposes since the Linux version of the academic
    license only allows execution of an already built model. In
    addition, Linux does not support excel file import and export. For
    more information of AIMMS Linux command-line run, refer to the
    [Release Notes for
    Linux](https://download.aimms.com/aimms/download/data/ReleaseNotes/AIMMS_release-Linux.pdf).

How to Run a Model {#How_to_Run}
------------------

To run a deterministic UC model, follow these steps in the following
order:

1.  Right-click on `MainInitialization` and press `Run Procedure`

2.  Right-click on `ReadFromExcel` and press `Run Procedure` and wait
    until loaded

3.  Right-click on `MainExecution` and press `Run Procedure` and wait
    for the programme to finish running (optimising)

The user has some options to interact with the model during this step:

-   Press `Ctrl+P` to see the execution progress window
    (Figure [progress~w~indow])

-   Press `Ctrl+shift+s` to terminate the programme execution

-   Press `Alt+F6` to debug the programme

When `MainExecution` is complete, the following steps should be followed
to generate the output:

1.  Right-click on `RunExternalProcedure` and press `Run Procedure`:
    outputs will be created in the designated folder

2.  Right-click on `MPStringExport` and press `Run Procedure`.
    Mathematical programme outputs will be created in the designated
    folder

These steps can be followed if the model user has everything set up
correctly and needs only to generate output of results. If the user
needs to change the model (refer to Subsection [Changing]) and set up a
new model, then change of inputs and some calibration in the model
should be performed (described beneath).

![image](progress_window.png) [progress~w~indow]

Global Input Parameters {#global_input_parameters}
=======================

There are some input parameters that are universal for all type of
modelling options discussed in Section [optimisation~o~ptions]. Input
parameters are located inside `Input Parameters` declaration (Figure
[input~p~arameters]).

![Input Parameters](input_parameters.png "fig:") [input~p~arameters]

Global parameters are always specified but not always used. Some of them
might refer to a specific technology, such as `StorageCap(sg)` for
energy storage or `RAS_charge_rate_s` for NGCC-PCC. Not always are all
technologies included in the optimisation run and therefore having their
parameters correctly inserted at all times will help later try different
fleet of technologies.\
Each parameter has the following fields that can be filled:

-   **Identifier**\
    This is basically the name of the parameter. Make sure to name
    parameters in convenient conventions. The author prefers either
    combining words together without any space in between (with the
    second word starting in capital letter), such as `carbonCost` and/or
    combining them with underscores, such as `RAS_charge_rate_s`.

-   **Index domain**\
    This is basically index pertaining to a specific set/s declared
    under `set` declaration (more about sets later in Section [Sets]).
    Note that index domain can be equally zero-dimensional (in other
    words, *scalar*), one-dimensional or multidimensional depending on
    the parameter type. An example of a scalar is `carbonCost`, an
    example of a one-dimensional parameter is `storageLevelCap(sg)` and
    an example of a multidimensional parameter is `rate(f,pccs,t,d,l)`.
    To put the desired index in the field, use provided wizard button
    next to it in order to navigate through the `Index Domain Wizard`
    window. Choose your desired domain set by clicking the wizard button
    associated with `Domain Set` field.

-   **Text**\
    This is basically the description of the parameter. Put a short
    description here. For longer descriptions or thoughts or
    explanations or draft definitions, use designated `Comment` area at
    the bottom of the screen (see the last bullet point!).

-   **Range**\
    This is basically the numerical range of the parameter. Use wizard
    button to open `Range Wizard` window and choose between
    `Standard Range`, i.e. ranges that are normally used in most
    optimisation problems and `User Defined`, i.e. ranges where you are
    able to specify bounds of your `Continuous` or `Integer` parameter
    [^1].

-   **Unit**\
    This is a field for a scale factor and most of the time is not used
    in UC models. For more information, refer to [Units of
    Measurement](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_UnitsOfMeasurement.pdf).

-   **Default**\
    This is a field for a default value of the parameter before it can
    later be assigned a different value (compare with `Definition` and
    `Initial data`).

-   **Property**\
    This field is for advanced versions of the deterministic model, such
    as Stochastic UC or Robust UC (for more information, refer to
    Appendix [SUC] and [RUC]). Use this property type only if you want
    to solve the stochastic or robust counterpart of your deterministic
    model. AIMMS makes it easy to run stochastic model when you’ve
    already built your deterministic model; you only need to specify
    which of your parameters are stochastic by using the
    `Parameter Type` field after opening Property wizard. For more
    information on properties and attributes as well as stochastic and
    robust optimisation, refer to AIMMS [Parameter
    Declaration](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_ParameterDeclaration.pdf)
    and [Stochastic
    Programming](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_StochasticProgramming.pdf)
    and [Robust
    Optimisation](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_RobustOptimization.pdf).

-   **Definition**\
    This is a sub-field for inserting parameter data (compare with
    `Definition` attribute of `Variable` or `Constraint` in Section
    [math~m~odel]) that cannot be changed throughout the model. When
    defining one-dimensional data, follow the structure shown below to
    assign specific values corresponding to set data:

            data { 
            PHS:            5,
            CAES:           0.4,
            Flywheel:       0.00025,
            Flow_Battery:       0.01,
            Hydrogen_Fuel_Cell: 0.05}
            

    The above definition is for `StorageCap(sg)` parameter defining the
    ramping capacity of each storage technology[^2]. Don’t forget to
    enclose your data inside `data{}`.

-   **Initial data**\
    This is a field for storing initial data. It’s not necessary to use
    this field as the parameters can be later initialised inside
    `MainInitialization` declaration.

-   **Comment**\
    This is a field for inserting anything helpful for the modeller;
    it’s not a part of the modelling process.

Input Files
===========

Files used in the model should be put in the same directory as the
model. These files presented below are necessary for the functioning of
the model:

-   `capacity_data_vitali_MIP_pw`\
    This is the file of all operational data on generators.

-   `demand_2010`\
    This is the file including hourly demand data in year 2010, given as
    day clusters. When running the model with this data chosen, make
    sure to use *day-by-day* optimisation option described in subsection
    [daily].

-   `demand_2010_1week`\
    This is the file including hourly demand data in year 2010, given as
    weekly clusters. When running the model with this data chosen, make
    sure to use weekly optimisation option described in subsection
    [weekly].

-   `demand_2010_2week`\
    This is the file including hourly demand data in year 2010, given as
    two-weekly clusters. When running the model with this data on, make
    sure to use *two-weekly* optimisation option described in subsection
    [2weekly].

-   `DP_DEMAND_WIND_2002_2010_Solar`\
    This is the file including hourly demand, offshore wind, onshore
    wind, solar penetration levels – using multiple analysis and
    re-analysis databases – for different installed renewable capacity
    which the modeller can use. Currently, this file includes data from
    years 2002 to 2010 but can be easily upgraded to include more recent
    data.

-   `Fuel spreadsheet`\
    This is a file containing start-up and running fuel for each
    technology. This is only used for doing Monte-Carlo simulation
    optimisation to find the distribution of a specific outcome (*e.g.*
    distribution of energy storage profit) with respect to fuel-price
    uncertainty. By default, it uses only mean fuel prices given in
    Column B which can be changed with latest fuel-price projections.

-   `res_UP`\
    This is a file for hourly deterministic upward reserve in year 2010,
    given as day clusters. When running the model with this data chosen,
    make sure to use *day-by-day* optimisation option described in
    Subsection [daily].

-   `res_UP_1week`\
    This is the file including hourly deterministic upward reserve in
    year 2010, given as weekly clusters. When running the model with
    this data chosen, make sure to use *weekly* optimisation option
    described in Subsection [weekly].

-   `res_UP_2week`\
    This is the file including hourly deterministic upward reserve data
    in year 2010, given as two-weekly clusters. When running the model
    with this data chosen, make sure to use *two-weekly* optimisation
    option described in Subsection [2weekly].

-   `solar_LF`\
    This is a file for hourly deterministic solar load factors in year
    2010, given as day clusters. When running the model with this data
    chosen, make sure to use *day-by-day* optimisation option described
    in Subsection [daily].

-   `solar_LF_1week`\
    This is the file including hourly deterministic solar load factors
    in year 2010, given as weekly clusters. When running the model with
    this data chosen, make sure to use *weekly* optimisation option
    described in Subsection [weekly].

-   `solar_LF_2week`\
    This is the file including hourly deterministic solar load factors
    in year 2010, given as two-weekly clusters. When running the model
    with this data chosen, make sure to use *two-weekly* optimisation
    option described in Subsection [2weekly].

-   `wind_LF`\
    This is a file for hourly deterministic load factors for both
    offshore and onshore wind in year 2010, given as day clusters. When
    running the model with this data chosen, make sure to use
    *day-by-day* optimisation option described in Subsection [daily].

-   `wind_LF_1week`\
    This is the file including hourly deterministic load factors for
    both offshore and onshore wind in year 2010, given as weekly
    clusters. When running the model with this data chosen, make sure to
    use *weekly* optimisation option described in Subsection [weekly].

-   `wind_LF_2week`\
    This is the file including hourly deterministic load factors for
    both offshore and onshore wind in year 2010, given as two-weekly
    clusters. When running the model with this data chosen, make sure to
    use *two-weekly* optimisation option described in Subsection
    [2weekly].

These input files are read in an external procedure called
`ReadFromExcel` (Figure [ReadFromExcel]) where necessary amendments
should be done in order to set the correct optimisation option as
described in `Input files` paragraph under Subsection [daily].

![ReadFromExcel](ReadFromExcel.png "fig:") [ReadFromExcel]

Sets {#Sets}
====

This declaration includes all sets used throughout the model, such as
generator sets, time intervals set. The model requires different sets
for different technologies, such as sets of `ThermalGenerators` or
`StorageGenerators`. Similarly, the model requires sets of
`DemandProfiles` and `DemandPeriods` where the model user makes
necessary changes to choose the right number of clusters and number of
hours per cluster considered in the optimisation model.\
Before running the model, make sure that the correct number of clusters
have been chosen in `DemandProfiles`. To run the model under
*day-by-day* optimisation ([daily]) for the first 7 days, put
`data{C1..C7}` inside `Definition` field. To run for the first 2 weeks
if *weekly* optimisation ([weekly]) is chosen, put `data{C1..C2}`.
Similarly for `DemandPeriods` set: if *day-by-day* optimisation
([daily]) is chosen, put `data{1 .. 24}` and if *weekly* optimisation
([weekly]) is chosen, put `data{1..168}`.\
The model incorporates different sets (groups) of generating
technologies. The basis of grouping those technologies is to combine
*similar* technologies together to help the construction of relevant
model constraints.\
Model user needs to adjust only the following generator sets:

-   `NonDispatchableGenerators`

-   `BaseloadGenerators`

-   `PCCSGenerators`

-   `CCGTGenerators`

-   `OCGTGenerators`

-   `StorageGenerators`

-   `ConsumerGenerators`

-   `AirSeparationUnits`

-   `ACGenerators`

By adjusting, it is meant that the user can choose any subset of given
generator type. For example, if we want to choose only 5 CCGT generators
in our model out of 40 available, we need to comment out the rest of the
generators – *i.e.* by putting an exclamation mark (!) in the correct
place – in the following way:

{\
\
}

The rest of the generator sets are formed by some combination of the
above sets, *e.g.* `GeneratorTypes` is formed by all above-mentioned
generators, `PhysicalGenerators` is formed by those generators that
physically exist and do actually generate electricity:

    GeneratorTypes - AirSeparationUnits - ConsumerGenerators

*i.e.* they include all generators apart from air separation units
(units associated with Allam Cycle plants) and consumer generators
(demand response which is represented as pseudo generators).\
The next sets that the user should pay attention to are sets associated
with UC mathematical programming types. Two modelling options are
implemented in this package with their associated variable and
constraint set declarations:

1.  Quick Dispatch (qd)\
    Associated sets: `qdVariables`; `qdConstraints`

2.  Piece-wise Linear Approximation of Quadratic Fuel Function (pw)\
    Associated sets: `pwVariables`; `pwConstraints`

For more information about differences of these two models, refer to
@wood2014power and @huang2017electrical.

To choose the right option for your model, you should follow the
procedure described in Chapter [math~m~odel].

Model Initialisation
====================

To initialise a model, make sure that parameters and element parameters
in `Initialisation Parameters` declaration (Figure
[Initialisation~P~arameters]) are all set and later correctly
initialised inside `MainInitialization` (Figure [MainInitialization]) or
inside `MainExecution` (Figure [MainExecution]).

<span>.55</span> ![image](Initialisation_Parameters.png)
[Initialisation~P~arameters]

<span>.77</span> ![image](MainExecution.png) [MainExecution]

![MainInitialization](MainInitialization.png "fig:")
[MainInitialization]

Most of initialisation parameters are either binary or integer types
which switch on/off a specific feature for a model run. For instance,
the parameter `Active` defines which constraints/variables are active in
a specific model if it is set to one and inactive if set to zero.

Use of parameter *Active*
:   Sometimes the user would like to run a sub-problem – meaning that
    some constraints and variables will be included and some will not.
    In this case, the parameter `Active` or `Active` inside
    `Index domain` of a constraint/variable will make sure it is
    included or excluded from the bundle of constraints/variables
    (Figure [not~A~ctive]).

![Use of *Active* parameter for variable
*Status\_Stopped*](not_Active.png "fig:") [not~A~ctive]

Optimisation Options {#optimisation_options}
====================

[Opt-Options] Different solution methods can be chosen for the same
problem. The choice of a method depends on many factors. Most
importantly, the modeller ought to know whether exact solutions are
needed or heuristics will suffice.\
The following subsections present the list of five options that have
been developed (or are under development – options in subsections
[continuous] and [rolling~h~orizon]) which are generally used in UC
models [^3]. The algorithm should be run on Gurobi 7.0 (or higher)[^4]
or CPLEX 12.7 (or higher) solver linked to AIMMS algebraic modelling
language. If a specific solver is missing from

    Settings->Solver Configuration...

then its [Dynamic Link Library
(DLL)](https://support.microsoft.com/en-gb/help/815065/what-is-a-dll)
file should be added. The procedure to link a specific solver to AIMMS
is described in this [Knowledge
Base](https://aimms.com/english/developers/resources/knowledge-base/kb00002/).
After linking the required solver to solve UC model, make sure that the
solver is checked (selected) to run MIP and LP optimisation classes.

Day-by-Day {#daily}
----------

This option performs decomposition of yearly (or any sub-duration) power
scheduling into successive *daily* optimal scheduling by running the
optimisation model for each day in succession and combining the results
at the end. It utilises a branch-and-bound algorithm @cohen1983branch
and reaches [zero optimality
gap](http://www.gurobi.com/resources/getting-started/mip-basics). In
spite of the fact that the problem is solved for each separate day
(cluster), with a careful modelling it was possible to preserve all
minimum up and down times and start-up and shut-down costs whenever the
model transitions from one day (cluster) to another.

Parameter initialisation
:   To initialise *day-by-da*y optimisation option, the modeller needs
    to set the following inside the `MainInitialization` (Figure
    [MainInitialization]):

        optimis_horizon_option              := 0;

Input files
:   Depending on the optimisation method, the input files may change.
    All required files are placed in the same directory as the model and
    every time the programme is initialised, the correct files are
    read.\
    Input demand data for this option are located in an excel file named
    `demand_2010`. This is a 24-row and 365-column matrix of gross
    demand data representing hourly national electricity demand of each
    day in year 2010. Although all daily demand data are given in the
    file, any subset of consecutive days can be chosen. For example, if
    we want to use only the first seven-day data in our optimisation
    model, then `ReadFromExcel` procedure should have demand and weight
    of each day (cluster) blocks adjusted accordingly under
    `if (optimis_horizon_option<3) then` statement:

        if axll::WorkBookIsOpen("demand_2010.xlsx") then
        axll::SelectWorkBook("demand_2010.xlsx");
        else
        axll::OpenWorkBook("demand_2010.xlsx");
        endif;
        axll::SelectSheet("Sheet1");
        axll::ReadSet(
            SetReference:DemandPeriods,
            SetRange:"A2:A25",
            ExtendSuperSets:1);
        axll::ReadTable(
            IdentifierReference:demand,
            RowHeaderRange:"A2:A25",
            ColumnHeaderRange:"B1:H1",
            DataRange:"B2:H25");

        !weight of each cluster
        if axll::WorkBookIsOpen("demand_2010.xlsx") then
        axll::SelectWorkBook("demand_2010.xlsx");
        else
        axll::OpenWorkBook("demand_2010.xlsx");
        endif;
        axll::SelectSheet("Sheet1");
        axll::ReadSet(
            SetReference:Years,
            SetRange:"A27",
            ExtendSuperSets:1);
        axll::ReadTable(
            IdentifierReference:weight_,
            RowHeaderRange:"A27",
            ColumnHeaderRange:"B26:H26",
            DataRange:"B27:H27");

    The values in the first block that are subject to change are `B1:H1`
    and `B2:H25` corresponding to the first and seventh days in an excel
    input file for `ColumnHeaderRange` and `DataRange`, respectively. In
    the second block, i.e. `weight of each cluster`, changeable values
    are `B26:H26` and `B27:H27` for `ColumnHeaderRange` and `DataRange`,
    respectively.\
    Similar changes should be performed for the `solar_LF_2010`,
    `wind_LF_2010` and `reserve data` blocks by adjusting `B1:H1` and
    `B2:H25` for `ColumnHeaderRange` and `DataRange`, respectively.

Continuous
----------

[continuous] This option hasn’t been tested vigorously, so the author
suggests against its use.

Rolling Horizon
---------------

[rolling~h~orizon]

Not yet implemented.

Two-weekly {#2weekly}
----------

This option performs decomposition of yearly (or any sub-duration) power
scheduling into successive *two-weekly* optimal scheduling by running
the optimisation model for each two-weeks in succession and combining
the results at the end. It utilises a branch-and-bound algorithm
@cohen1983branch and reaches [zero optimality
gap](http://www.gurobi.com/resources/getting-started/mip-basics). In
spite of the fact that the problem is solved for each separate two-weeks
(cluster), with a careful modelling it was possible to preserve all
minimum up and down times and start-up and shut-down costs whenever the
model transitions from one two-weeks (cluster) to another.

Parameter initialisation
:   To initialise *two-weekly* optimisation option, the modeller needs
    to set the following inside the `MainInitialization` (Figure
    [MainInitialization]):

            optimis_horizon_option              := 3;
            

Input files
:   Depending on the optimisation method, the input files may change.
    All required files are placed in the same directory as the model and
    every time the programme is initialised and correct files are read.\
    Input demand data for this option are located in an excel file named
    `demand_2010_2week`. This is a 336-row and 26-column matrix of gross
    demand data representing hourly national electricity demand of each
    two-weeks in year 2010 [^5]. Although all two-weekly demand data are
    given in the file, any subset of consecutive two-weeks can be
    chosen. For example, if we want to use only the first two-weeks data
    [^6] in our optimisation model, then `ReadFromExcel` procedure
    should have demand and weight of each two-weeks (cluster) blocks
    adjusted accordingly under `elseif (optimis_horizon_option=3) then`
    statement:

        if axll::WorkBookIsOpen("demand_2010_2week.xlsx") then
        axll::SelectWorkBook("demand_2010_2week.xlsx");
        else
        axll::OpenWorkBook("demand_2010_2week.xlsx");
        endif;
        axll::SelectSheet("Sheet1");
        axll::ReadSet(
            SetReference:DemandPeriods,
            SetRange:"A2:A337",
            ExtendSuperSets:1);
        axll::ReadTable(
            IdentifierReference:demand,
            RowHeaderRange:"A2:A337",
            ColumnHeaderRange:"B1:B1",
            DataRange:"B2:B337");

        !weight of each cluster
        if axll::WorkBookIsOpen("demand_2010_2week.xlsx") then
        axll::SelectWorkBook("demand_2010_2week.xlsx");
        else
        axll::OpenWorkBook("demand_2010_2week.xlsx");
        endif;
        axll::SelectSheet("Sheet1");
        axll::ReadSet(
            SetReference:Years,
            SetRange:"A339",
            ExtendSuperSets:1);
        axll::ReadTable(
            IdentifierReference:weight_,
            RowHeaderRange:"A339",
            ColumnHeaderRange:"B338:B338",
            DataRange:"B339:B339");

    The values in the first block that are subject to change (for
    inclusion of more two-weeks) are `B1:B1` and `B2:B337` corresponding
    to the first two-weeks in an excel input file for
    `ColumnHeaderRange` and `DataRange`, respectively. In the second
    block, i.e. `weight of each cluster`, changeable values are
    `B338:B338` and `B339:B339` for `ColumnHeaderRange` and `DataRange`,
    respectively.\
    Similar changes should be performed for the `solar_LF_2010`,
    `wind_LF_2010` and `reserve data` blocks by adjusting `B1:B1` and
    `B2:B337` for `ColumnHeaderRange` and `DataRange`, respectively.

Weekly
------

This option performs decomposition of yearly (or any sub-duration) power
scheduling into successive *weekly* optimal scheduling by running the
optimisation model for each week in succession and combining the results
at the end. It utilises a branch-and-bound algorithm @cohen1983branch
and reaches [zero optimality
gap](http://www.gurobi.com/resources/getting-started/mip-basics). In
spite of the fact that the problem is solved for each separate week
(cluster), with a careful modelling it was possible to preserve all
minimum up and down times and start-up and shut-down costs whenever the
model transitions from one week (cluster) to another.

Parameter initialisation
:   To initialise *weekly* optimisation option, the modeller needs to
    set the following inside the `MainInitialization` (Figure
    [MainInitialization]):

            optimis_horizon_option              := 4;
            

Input files
:   Depending on the optimisation method, the input files may change.
    All required files are placed in the same directory as the model and
    every time the programme is initialised and files are read.\
    Input demand data for this option are located in an excel file named
    `demand_2010_1week`. This is a 168-row and 52-column matrix of gross
    demand data representing hourly national electricity demand of each
    week in year 2010. Although all weekly demand data are given in the
    file, any subset of consecutive weeks can be chosen. For example, if
    we want to use only the first week data [^7] in our optimisation
    model, then `ReadFromExcel` procedure should have demand and weight
    of each week (cluster) blocks adjusted accordingly under
    `elseif (optimis_horizon_option=4) then` statement:

        if axll::WorkBookIsOpen("demand_2010_1week.xlsx") then
        axll::SelectWorkBook("demand_2010_1week.xlsx");
        else
        axll::OpenWorkBook("demand_2010_1week.xlsx");
        endif;
        axll::SelectSheet("Sheet1");
        axll::ReadSet(
            SetReference:DemandPeriods,
            SetRange:"A2:A169",
            ExtendSuperSets:1);
        axll::ReadTable(
            IdentifierReference:demand,
            RowHeaderRange:"A2:A169",
            ColumnHeaderRange:"B1:B1",
            DataRange:"B2:B169");
            
        !weight of each cluster
        if axll::WorkBookIsOpen("demand_2010_1week.xlsx") then
        axll::SelectWorkBook("demand_2010_1week.xlsx");
        else
        axll::OpenWorkBook("demand_2010_1week.xlsx");
        endif;
        axll::SelectSheet("Sheet1");
        axll::ReadSet(
            SetReference:Years,
            SetRange:"A171",
            ExtendSuperSets:1);
        axll::ReadTable(
            IdentifierReference:weight_,
            RowHeaderRange:"A171",
            ColumnHeaderRange:"B170:B170",
            DataRange:"B171:B171");

    The values in the first block that are subject to change (for
    inclusion of more weeks) are `B1:B1` and `B2:B169` corresponding to
    the first week in an excel input file for `ColumnHeaderRange` and
    `DataRange`, respectively. In the second block, i.e.
    `weight of each cluster`, changeable values are `B170:B170` and
    `B171:B171` for `ColumnHeaderRange` and `DataRange`, respectively.\
    Similar changes should be performed for the `solar_LF_2010`,
    `wind_LF_2010` and `reserve data` blocks by adjusting `B1:B1` and
    `B2:B169` for `ColumnHeaderRange` and `DataRange`, respectively.

Mathematical Model {#math_model}
==================

Mathematical model can be found in `Declaration Math Program`
(Figure [Declaration~M~ath~P~rogram]). You’ll find all variables(),
constraints() and mathematical program types() in this declaration.

![Declaration Math Program](Declaration_Math_Program.png "fig:")
[Declaration~M~ath~P~rogram]

When deciding on which mathematical program type to use, make sure to
put the correct variable and constraint sets inside math program
`vitali` (Figure [math~p~rogram]). In general, `qd` program types are
easier to solve, *i.e.* they consume less computational time, compared
to `pw` program types because they have less integer variables.

The objective function of the math program is declared as a in
`Declaration Math Program` and called in inside `Objective` field
(Figure [math~p~rogram]).\
When we talk about UC problem types (*i.e.* `qd` and `pw`[^8]), please
do not confuse with math programming problem types (*i.e.* Linear
Program (LP), Mixed Integer Program (MIP), Non-linear Program (NLP)
*etc.*[^9]). UC problems are solved using some math programming problem
type/s.

![Mathematical Program Setup](math_program.png "fig:") [math~p~rogram]

Variables
---------

Each variable has the following fields that can be filled:

-   **Identifier**\
    This is basically the name of the variable. Make sure to name
    variables in convenient conventions. The author prefers either
    combining words together without any space in between (with the
    second word starting in capital letter), such as
    `storageLevel(sg,t,d)` and/or combining them with underscores, such
    as `sg_lambdaLevel(sg,t,d)`.

-   **Index domain**\
    This is basically index pertaining to a specific set/s declared
    under `set` declaration (more about sets in Section [Sets]). Note
    that index domain can be equally zero-dimensional (mostly for
    defining objective function, *e.g.* `totalCost`), or
    multidimensional such as `output_(g,t,d)`. To put the desired index
    in the field, use provided wizard button next to it in order to
    navigate through the `Index Domain Wizard` window. Choose your
    desired domain set by clicking the wizard button associated with
    `Domain Set` field.

-   **Text**\
    This is basically the description of the variable. Put a short
    description here. For longer descriptions or thoughts or
    explanations or draft definitions, use designated `Comment` area at
    the bottom of the screen (see the last bullet point!).

-   **Range**\
    This is basically the numerical range of the variable. Use wizard
    button to open `Range Wizard` window and choose between
    `Standard Range`, i.e. ranges that are normally used in most
    optimisation problems and `User Defined`, i.e. ranges where you are
    able to specify bounds of your `Continuous` or `Integer` parameter
    [^10].

-   **Unit**\
    This is a field for a scale factor and most of the time is not used
    in UC models. For more information, refer to [Units of
    Measurement](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_UnitsOfMeasurement.pdf).

-   **Default**\
    This is a field for a default value of the variable before it can be
    assigned a different value later (compare with `Definition`).

-   **Property**\
    This field is mostly for collecting [sensitivity
    information](https://download.aimms.com/aimms/download/manuals/AIMMS3OM_SensitivityAnalysis.pdf)
    about variables, such as `Reduced Cost`[^11] which is the marginal
    change in the objective function when decision variable is also
    changed marginally @luenberger2008linear. It can however be used if
    you are solving an advanced versions of the deterministic model,
    such as Stochastic UC or Robust UC (refer to Appendix [SUC] and
    [RUC] for more information). In this case there might be a need to
    specify also your variables to be stochastic in `Variable Type`
    field of `Property Wizard`. Use this property type only if you want
    to solve the stochastic or robust counterpart of your deterministic
    model. AIMMS makes it easy to run stochastic model when you’ve
    already built your deterministic model; you only need to specify
    which of your parameters and variables are stochastic by using the
    `Parameter Type` or `Variable Type` field after opening Property
    wizard. For more information on properties and attributes as well as
    stochastic and robust optimisation, refer to AIMMS [Parameter
    Declaration](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_ParameterDeclaration.pdf)
    and [Stochastic
    Programming](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_StochasticProgramming.pdf)
    and [Robust
    Optimisation](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_RobustOptimization.pdf)
    chapters.

-   **Priority**\
    This field is for specifying the priority of the variables among
    variables. The associated parameter is called
    `priority_parameter(ps)` located in `Initialisation Parameters`
    declaration. This separates all variables in 5 priority groups which
    are stacked according to their priority during optimisation run.
    Although useful in many optimisation setups where one knows that
    decision variables have a precedence over operational ones or
    start-up and shut-down decisions have precedence over dispatch
    decisions, the inclusion of this feature does not essentially
    increase the optimisation run time in the current UC models.\
    However, should the modeller decides to complicate the existing
    model further, there might be a need to prioritise start-up and
    shut-down decisions over operational ones.

-   **Nonvar status**\
    This field is for specifying the non-variable status of the variable
    if it is called as a parameter during a specific `Solve` statement
    (for more information, see [Optimization Modeling
    Components](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_VariableConstraintDeclaration.pdf)).

-   **Definition**\
    This is a field for defining the variable relationship with other
    variables (compare with `Definition` attribute of `Parameter` or
    `Constraint` in Section [global~i~nput~p~arameters] and Subsection
    [constraints]).

-   **Comment**\
    This is a field for inserting anything helpful for the modeller;
    it’s not a part of the modelling process.

Constraints
-----------

[constraints]

Each constraint has the following fields that can be filled:

-   **Identifier**\
    This is basically the name of the constraint. Make sure to name
    constraints in convenient conventions. The author prefers either
    combining words together without any space in between (with the
    second and third words *etc.* starting in capital letters), such as
    `eqSpinningMet(t,dd_i)` and/or combining them with underscores, such
    as `eqOxy_tank_level(ac,t,dd_i)`.

-   **Index domain**\
    This is basically index pertaining to a specific set/s declared
    under `set` declaration (more about sets in Section [Sets]). Note
    that index domain can be equally zero-dimensional (mostly for
    defining objective function, *e.g.* `calcTotalCost_pw`), or
    multidimensional such as `calcStarts1(g,t,dd_i)`. To put the desired
    index in the field, use provided wizard button next to it in order
    to navigate through the `Index Domain Wizard` window. Choose your
    desired domain set by clicking the wizard button associated with
    `Domain Set` field.

-   **Text**\
    This is basically the description of the constraint. Put a short
    description here. For longer descriptions or thoughts or
    explanations or draft definitions, use designated `Comment` area at
    the bottom of the screen (see the last bullet point!).

-   **Unit**\
    This is a field for a scale factor and most of the time is not used
    in UC models. For more information, refer to [Units of
    Measurement](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_UnitsOfMeasurement.pdf).

-   **Property**\
    This field is mostly for collecting [sensitivity
    information](https://download.aimms.com/aimms/download/manuals/AIMMS3OM_SensitivityAnalysis.pdf)
    about constraints, such as `Shadow Price`[^12] which is the impact
    of an incremental change in the right hand side of the constrain on
    the objective function @luenberger2008linear. It can however be used
    if you are solving an advanced versions of the deterministic model,
    such as Stochastic UC or Robust UC (for more information, refer to
    Appendix [SUC] and ). In this case there might be a need to specify
    also your constraints to be a `Chance Constraint` in
    `Property Wizard`. Use this property type only if you want to solve
    the stochastic or robust counterpart of your deterministic model.
    AIMMS makes it easy to run stochastic model when you’ve already
    built your deterministic model; you only need to specify which of
    your constraints are chance constraints. For more information on
    properties and attributes as well as stochastic and robust
    optimisation, refer to AIMMS [Parameter
    Declaration](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_ParameterDeclaration.pdf)
    and [Stochastic
    Programming](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_StochasticProgramming.pdf)
    and [Robust
    Optimisation](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_RobustOptimization.pdf)
    chapters.\
    Other useful features of constraint properties are `SOS 1` and
    `SOS 2` and `Indicator Constraint` types that can be specified. SOS
    stands for Set of Ordered Sets and can be used for constructing
    piece-wise linear approximation of quadratic fuel function[^13]
    @huang2017electrical. Constraints can also be declared as indicator
    constraints to replace as an alternative to Big-M method. However,
    having tried implementing them, the author has found some
    compilation errors with them and therefore advises against their
    use. However, in future AIMMS releases, these bugs might be fixed
    and can be preferable alternatives to Big-M formulations.

-   **Definition**\
    This is a field for defining the constraints including variable
    relationship with other variables (compare with `Definition`
    attribute of `Parameter` or `Variable` in Section
    [global~i~nput~p~arameters] and Subsection [variables]).

-   **Comment**\
    This is a field for inserting anything helpful for the modeller;
    it’s not a part of the modelling process.

Model Building with AMS
=======================

[ams] Model building can be performed without interacting with AIMMS IDE
if one prefers a GAMS-like[^14] modelling development. To do this, the
modeller needs to open the *.ams* file with Notepad or Notepad++ and
make all required changes. The files includes all declarations,
procedures, external procedures, modules and so on. Changes should be
directly implemented in the file. For instance, if we want to change the
model to include 8 clusters instead of 7 in `DemandProfiles` set, the
definition filed should be changed to:

    Set DemandProfiles {
        Text: "demand profiles (clustered)";
        Index: d;
        Definition: data { C1..C8 };
    }

Parameters can be changed in a similar fashion:

    Parameter lim_exec_time {
        Text: "limit execution time to some seconds";
        Default: 900;
    }

By default, the above parameter limits the execution time of each
optimisation run – in our case to 900 seconds. But it can be later
overridden with the following assignment in `MainInitialization`:

    ! How many seconds each MP should run?
    lim_exec_time                   := 500000;

If you have both IDE and *.ams* files open and you want to make changes
in *.ams* file, then first make changes there, then save and close the
file. The IDE should be closed at the same time and after re-opening the
IDE, you can see that the effects have taken place.

Output generation
=================

Outputs are generated inside `MainExecution` declaration starting from
`Carbon calculations` block. All conceivable output data are generated
here, namely in `Carbon calculations`, `Generete outputs` and
`retrieving math program descriptors` blocks. Output data are exported
to the folder contained in the model as a Comma Separated Values (CSV)
files after running `RunExternalProcedure` and `MPStringExport`
procedures (refer to Section [How~t~o~R~un] for complete steps for
running and producing the results.). To ease the problem of
differentiating output data, they are exported with a prefix `o5_`. This
prefix can be used to denote the model version. Here are some output
files that can be read as ’output files from the fifth version of the
model’ produced by `RunExternalProcedure`:

    o5_statsOnline
    o5_statsStorage
    o5_charging
    o5_onshore_wind_curtailment
    o5_math_program_numbers

For example, by opening already generated `o5_math_program_numbers` CSV
file with Microsoft Excel, you will find an output which will have this
structure:

    math_program_set            o5_math_program_numbers
    Objective_                  31915737.8
    LinearObjective             31915737.8
    Incumbent                   31915737.8
    BestBound                   31915737.8
    Iterations                  11998
    Nodes_                      1
    GenTime                     0.265
    SolutionTime                1.872
    SolverCalls                 14
    NumberOfConstraints         30433
    NumberOfVariables           17305
    NumberOfNonzeros            92737
    NumberOfIntegerVariables    10488

Progress staus and solver status descriptors are exported as an *.out*
file via running `MPStringExport` procedure. The ouptut file can be
opened again with the help of Notepad++. An example of this output is
given below:

    o5_math_program_string(mp) := 
    data { 
          ProgramStatus : "Optimal",  
          SolverStatus : "NormalCompletion" 
          } ;

Some auxiliary files are also created in MatLab (M files) to convert
some of the AIMMS output files into more readable formats for further
analyses. Those M files are:

-   `conv_AIMMS_to_MatLab`

-   `csvwrite_with_headers`

which transform corresponding `o5_` files into `output_base`;
`output_base`; `starts`; `shuts`; `online`; `status_down`; `reserve`;
`turndown`; `extra_capacity`; `rampUP` and `rampDN` files. Follow the
instructions written in the M file `conv_AIMMS_to_MatLab` to generate
the desired post-output files by adjusting the correct number for
generators, clusters and iterations. Make sure also to adjust string `h`
in `conv_AIMMS_to_MatLab` file containing all considered technology
names.

References
==========

Advanced UC models
==================

Stochastic Unit Commitment
--------------------------

[SUC] Stochastic UC models assume that some parameters and decision
variables are stochastic. You can specify which parameters and variables
are stochastic by selecting appropriately `Parameter Type` and
`Variable Type` to be `Stochastic` after opening the associated
`Property` wizard. There is no need to change your deterministic model
in order to run the stochastic counterpart; AIMMS automatically
generates extra constraints associated with the stochastic variables and
parameters. It transforms the objective cost (profit) function into
expected cost (profit) function with recourse (for more information
about stochastic programming with recourse, refer to
@birge2011introduction for general programs, and to @kall2011stochastic
for linear stochastic programs).\
Here we will model and solve only two-stage stochastic unit commitment
problem. However, the formulation of multi-stage problem is very
straightforward. One essential part of building the stochastic
equivalent of the deterministic model is to specify the period-to-stage
mapping. In two-stage formulation, it is assumed that plant on/off
decisions are made at the end of the first stage and expected
values[^15] of stochastic parameter data from demand, wind and solar are
used. Dispatch decisions are made at the end of the second stage after
the realisation of stochastic events from demand and solar & wind load
factors during the second stage. Therefore, the period-to-stage mapping
is done with the following commands in `StochasticProcedures`:

    DemandPeriodToStageMapping('1',t)  := 1;
    DemandPeriodToStageMapping('2',t)  := 2;

    CommitmentStage(t) := DemandPeriodToStageMapping('1',t);
    DispatchStage(t)   := DemandPeriodToStageMapping('2',t);

At the second stage, in this setting, the stochastic parameters either
take high value (H) or low value (L)[^16]. At each hour of the second
stage, demand can randomly jump up to 120% of its expected value in
scenario H or down to 80% of its expected value in scenario L.
Similarly, at each hour of the second stage, solar load factors can
randomly jump up to 140% of their expected value in scenario H or down
to 60% of their expected value in scenario L. Wind load factors, on the
other hand, are assumed to randomly jump up to 150% of their expected
value in scenario H or down to 50% of their expected value in scenario
L.\
The above is achieved by putting the following code in the body of
`InitializeStochasticDataCallback`.

    for ( t | CommitmentStage(t) = CurrentStage) do
        demand.Stochastic(Scenario,t,d) := demand(t,d);
        solar_LF.Stochastic(Scenario,t,d):= solar_LF(t,d);
        wind_LF.Stochastic(Scenario,t,d):= wind_LF(t,d);
    endfor;

    for ( t | DispatchStage(t) = CurrentStage) do
        demand.Stochastic(Scenario,t,d) := 
        if(ChildBranch = 1) then 
         Uniform(1,1.2) * demand(t,d)!Uniform(40,50)!High demand level
        else !i.e. (ChildBranch =2)
         Uniform(0.8,1) * demand(t,d)!Uniform(30,40)!Low demand level
        endif;
        
        solar_LF.Stochastic(Scenario,t,d):= 
        if(ChildBranch = 1) then 
         Uniform(1,1.4) * solar_LF(t,d)!Uniform(40,50)!High demand level
        else !i.e. (ChildBranch =2)
         Uniform(0.6,1) * solar_LF(t,d)!Uniform(30,40)!Low demand level
        endif;
        
        wind_LF.Stochastic(Scenario,t,d):= 
        if(ChildBranch = 1) then 
         Uniform(1,1.5) * wind_LF(t,d)!Uniform(40,50)!High demand level
        else !i.e. (ChildBranch =2)
         Uniform(0.5,1) * wind_LF(t,d)!Uniform(30,40)!Low demand level
        endif;
    endfor;

Each branch is considered equally possible:

    return /*relative weight*/ 1;

It is possible also to adjust the relative weights of each branch.\
Have a look also at the body of `InitializeNewScenarioCallback` and
`InitializeChildBranchesCallback` for new scenario and child-branch
generation procedures.

### Distribution-based Scenario Generation (Branching)

[DSUC]

#### How to Run a Model {#How_to_Run_Stoch}

To run the existing model, follow these steps in this order:

1.  Right-click on `MainInitialization` and press `Run Procedure`

2.  Right-click on `ReadFromExcel` and press `Run Procedure` and wait
    until loaded

3.  Right-click on `StochasticProcedures` and press `Run Procedure`

4.  Right-click on `SolveStochasticUC` and press `Run Procedure` and
    wait for the programme to finish running (optimising)

If you have a deterministic model with its objective variable
`totalCost` declared without its `Definition` field, you need to fill
this definition field when running the stochastic model. Pay attention
to what type of UC model you are solving; if you want to solve *quick
dispatch*, then copy-paste the definition field from `calcTotalCost_qd`
constraint after the equality sign. Respectively, copy-paste the
definition field (after the equality sign) from `calcTotalCost_pw`
constraint if you want to solve the *piece-wise approximation* type.
Don’t forget to change the model type in *vitali* as well.\
Similar to the deterministic model, the user has some options to
interact with the stochastic model during step 4:

-   Press `Ctrl+P` to see the execution progress window (similar to the
    one in Figure [progress~w~indow])

-   Press `Ctrl+shift+s` to terminate the programme execution

-   Press `Alt+F6` to debug the programme

When `SolveStochasticUC` is complete, the following step should be
followed to generate the output:

1.  Right-click on `RunStochasticResults` and press `Run Procedure`:
    outputs will be created inside AIMMS.

The output parameters can be viewed by right-clicking on them and
pressing `Data...`[^17]\
These output results later can be assigned externally to files located
in the same folder as the model. These steps can be followed if the user
has all set up correctly and needs only to generate output of results.
If the user needs to change the model (refer to [Changing]) and set up a
new model, then change of inputs and some calibration in the model
should be performed.

### Scenario-based Tree Generation (Data Bundling)

[SSUC] This is not covered in this version of the manual. However, the
author aims to cover it in upcoming releases of the *User Manual*.
However, for an advance use of the models, you may contact the author or
refer to [this presentation by
AIMMS](https://aimms.com/files/5614/4795/0251/AIMMS_OptimizationUnderUncertainty_OListes_min.compressed.pdf)
or [AIMMS Language
Reference](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_StochasticProgramming.pdf).

### Benders Decomposition

[BSUC] [SSUC] This is not covered in this version of the manual.
However, the author aims to cover it in upcoming releases of the *User
Manual*. However, for an advance use of the models, you may contact the
author or read [AIMMS Language
Reference](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_StochasticProgramming.pdf).

Robust Unit Commitment
----------------------

[RUC] This is not covered in this version of the manual. However, the
author aims to cover it in upcoming releases of the *User Manual*.
However, for an advance use of the models, you may contact the author or
refer to [this presentation by
AIMMS](https://aimms.com/files/5614/4795/0251/AIMMS_OptimizationUnderUncertainty_OListes_min.compressed.pdf)
or [AIMMS Language
Reference](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_RobustOptimization.pdf)
.

Bi-level Optimisation
---------------------

[bi-level] Although not covered in this version of the manual, it is
implemented in the latest model distribution. The author aims to cover
the full description in upcoming releases of the *User Manual*.\
An example that has been implemented so far is the iteration-based
bi-level optimisation of system cost minimisation and CCS plant profit
maximisation. The model starts by minimising overall system cost and
finding respective shadow prices of relaxed MIP model at each hour of a
given cluster[^18]. Then these prices are passed to CCS plant operators
(*i.e.* they are taken as given by CCS plant operators) who decide to
operate their capture plants either:

-   in *bypass* mode, *i.e.* capture plant is not used and only fixed
    output penalty is incurred thus increasing overall CCS plant output
    – this generally happens at high electricity prices

-   by *charging* rich amine storage tank, *i.e.* solvent regeneration
    cycle is not used as rich solvent is stored in a tank for a later
    use – this happens at relatively high electricity prices

-   by *discharging* rich amine storage tank – this happens at low
    electricity prices

-   by *regenerating* solvent at a steady state – this happens at
    close-to-average electricity prices

After CCS plant operators decide their capture plant operating schedules
– which actually defines the maximum possible output (*net* output) that
the whole CCS plant can produce at each hour – under the given
electricity prices, the system operator takes these adjustments by CCS
plant operators and minimises the system cost again. After getting the
adjusted shadow prices, the system operator again passes them to CCS
plant operators. This loop repeats as many times as required to iterate
in order to reach an equilibrium state.\
For more advance use of these type of models, you may contact the
author.

Bespoke UC Models
-----------------

[bespoke] Those models are tailored specifically for solving UC models
with challenging technologies. Those technologies include but not
limited to:

-   Allam-Cycle oxy-combustion plants which are near-zero-carbon
    generation plants that use an innovative CO2 cycle by sending the
    compressed CO2 to transportation and storage system (AC)

-   post-combustion CO2 capture plants retrofitted to combined-cycle gas
    plants (NGCC-PCC)

#### UC with Oxy-Combustion Plants {#Allam_Cycle}

To run the model with AC plants, the user needs to activate
`ACGenerators` and `AirSeparationUnits` sets by commenting in/out the
number of AC plants and ASUs needed in the model (refer to Section
[Sets]).\
Associated `Initialisation Parameters` are:

-   parameter `AC_ASU_coupled`

-   parameter `Init_Oxy_tank_level(t)`

-   element parameter `map_AC_to_ASU(ac)`

Element parameter `map_AC_to_ASU(ac)` is later used in
`MainInitialization` to associate each AC plant with its ASU.\
Associated `Input Parameters` are:

-   `Oxy_tank_max_level`

-   `AC_continuation_penalty`

-   `AC_gasification_compression_penalty`

-   `ASU_oxygen_penalty`

-   `AC_liquefaction_penalty`

-   `AC_cooling_air_penalty`

-   `AC_heat_recovery_efficiency`

-   `eff_adder(ac)`

-   `fuel_recovery_dis_rate_adder`

Before running the model with AC plants, make sure you have the correct
input parameters for your AC plants. These plants can run with and
without oxygen storage which can be indicated with the following
assignment:

    AC_ASU_coupled                  := 1;

When `AC_ASU_coupled := 1`, it means that AC plants have their
associated ASUs and therefore oxygen storage option is used. When
`AC_ASU_coupled := 0`, then AC plants and ASUs are not associated[^19]
and therefore there is no oxygen storage. To associate each AC with its
ASU – assuming only 5 AC plants are available in the system – the
following mapping commands should be activated in `MainInitialization`:

    map_AC_to_ASU('Gas_CCS_AC_1')  := 'ASU_1'; 
    map_AC_to_ASU('Gas_CCS_AC_2')  := 'ASU_2'; 
    map_AC_to_ASU('Gas_CCS_AC_3')  := 'ASU_3'; 
    map_AC_to_ASU('Gas_CCS_AC_4')  := 'ASU_4'; 
    map_AC_to_ASU('Gas_CCS_AC_5')  := 'ASU_5';

When oxygen storage tank option is chosen, it can be further specified
whether the modeller wants some starting level of storage tank. For
example, if starting level of storage is 25% of its maximum capacity,
then:

    Init_Oxy_tank_level('1')            := 0.25 * Oxy_tank_max_level;

**NB:** Be aware that the execution of bespoke models might take longer
time to solve due to the presence of additional variables and
constraints.\

Although these additional variables and constraints are not presented
here, the modeller is advised to find them in the model and study them.\
For more information about the assumptions and modelling and workings of
an Allam Cycle plant, refer to the following paper:

-   *Highly flexible zero carbon electricity generation: An initial
    assessment of the value of Allam Cycle power plants with liquid
    oxygen storage in future GB electricity system*

#### UC with Post-Combustion CO2 Capture Plants {#PCCS}

This is a model for modelling the interim storage capability of a
post-combustion CO2 capture plant. CCS plants with interim storage
capability can be included in the generation mix to assess their
viability in future power systems. Interim storage is a basic form of a
small-scale grid-connected energy storage. It can be used to put off
available maximum electricity production by a CCS plant by capturing CO2
at a higher capture rates. Capturing CO2 is an energy-intensive process
and is therefore associated with high electricity output penalty; the
outcome of capturing is the reduced net output of overall CCS plant. The
capturing process can also be bypassed to avoid incurring electricity
penalty (or to reduce the penalty if operated at lower capture rates).
The outcome of not capturing (or capturing at lower rates) is the
increased net output of overall CCS plant which is the preferred state
when electricity prices are high.\
The model can be used to choose between options of having the interim
storage capability or not in CCS plants. If this is not initialised,
then:

    CCS_interim                 := 0;

The model can also be used for enabling or disabling *bypass* regime. If
this option is not initialised, then:

    CCS_bypass                  := 0;

When interim storage level is chosen, the modeller can further choose
whether some starting level of storage tank should be specified. For
example, if starting level of storage is 25% of its maximum capacity,
then:

    Init_RAS_level('1')                 := 0.25 * RAS_max_level;

For more information about the assumptions and modelling on interim
storage and operation of CCS plants, the user is advised to contact
Hannah Chalmers <hannah.chalmers@ed.ac.uk> and/or Mathieu Lucquiaud
<m.lucquiaud@ed.ac.uk>.

[^1]: Although anges might not be so essential for parameter
    declaration, they are very essential for variable declaration. For
    variable declaration, refer to Section [math~m~odel]

[^2]: Pay attention to the fact that **StorageCap(sg)** doesn’t have a
    dimension of time which means that storage technology ramping
    capacity is constant in the model. If you would like to make it time
    dependent, use StorageCap(sg,t) instead. Data can be read from an
    external database, such as **plant(g\_max,UniversalSet\_i)** or
    **demand(t,d)**.

[^3]: A brief description can be found in *MainInitialization* procedure
    inside *Model Explorer*.

[^4]: Average time it takes for Gurobi solver to reach the optimal
    solution for UC-type problems is faster than any other solver
    currently available for an academic use; therefore the author
    recommends using Gurobi at all times

[^5]: For a different year, data should be calculated separately and
    placed in this file

[^6]: **NB:** If you run model for more two-weeks, note that combined
    optimisation time including all considered two-weeks might become
    considerably long.

[^7]: **NB:** If you run model for more weeks, note that combined
    optimisation time including all considered weeks might become
    considerably long.

[^8]: Refer to fields *Constraints* and *Variables* in
    Figure [math~p~rogram]

[^9]: Refer to field *Type* in Figure [math~p~rogram].

[^10]: Ranges might not be so essential for parameter declaration, they
    are very essential for variable declaration though. For variable
    declaration, refer to Section [math~m~odel]

[^11]: The author recommends to have this option ticked for all
    variables.

[^12]: The author recommends having this option ticked for all
    variables.

[^13]: The author, however, has chosen a manual approach in constructing
    piece-wise linear functions.

[^14]: https://www.gams.com/

[^15]: Actually, those values in the current model are taken from year
    2010 which constitutes a medium year in terms of demand and weather
    data. However, the modeller is free to choose any base data as well
    as is free to choose [any statistical
    distributions](https://download.aimms.com/aimms/download/manuals/AIMMS3LR_DistributionsAndStatisticalOperators.pdf)
    available in AIMMS.

[^16]: It is easy to extend the branching to as many levels as need be.

[^17]: Make sure to choose *Table* as a *Type of Object* inside
    *Identifier* wizard window. Sometimes AIMMS doesn’t show the output
    in *Pivot Table* mode.

[^18]: A cluster can be a day, a week *etc.*

[^19]: In this case ASUs act as separate generators with miserable costs
    and outputs thus not effectively affecting the overall system cost
    results.
