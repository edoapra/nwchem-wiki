The PRINT and NOPRINT directives allow the user to control how much output NWChem generates. These two directives are special in that the compound directives for all modules are supposed to recognize them. Each module can control both the overall print level (general verbosity) and the printing of individual items which are identified by name (see below). The standard form of the PRINT directive is as follows:

```
PRINT [(none || low || medium || high || debug) default medium]  [<string list_of_names ... >]
NOPRINT <string list_of_names ... >
```

The default print level is medium.

Every output that is printed by NWChem has a print threshold associated with it. If this threshold is equal to or lower than the print level requested by the user, then the output is generated. For example, the threshold for printing the SCF energy at convergence is low. This means that if the user-specified print level on the PRINT directive is low, medium, high, or debug, then the SCF energy will be printed at convergence.

The overall print level specified using the PRINT directive is a convenient tool for controlling the verbosity of NWChem. Setting the print level to high might be helpful in diagnosing convergence problems. The print level of debug might also be of use in evaluating problem cases, but the user should be aware that this can generate a huge amount of output. Setting the print level to low might be the preferable choice for geometry optimizations that will perform many steps which are in themselves of little interest to the user.

In addition, it is possible to enable the printing of specific items by naming them in the PRINT directive in the <list_of_names>. Items identified in this way will be printed, regardless of the overall print level specified. Similarly, the NOPRINT directive can be used to suppress the printing of specific items by naming them in its <list_of_names>. These items will not be printed, regardless of the overall print level, or the specific print level of the individual items.

The list of items that can be printed for each module is documented as part of the input instructions for that module. The items recognized by the top level of the code, and their thresholds, are:

Name|Print Level|Description
---|---|---
"total time" | medium | Print cpu and wall time at job end
"task time" | high | Print cpu and wall time for each task
"rtdb" | high | Print names of RTDB entries
"rtdbvalues" | high | Print name and values of RTDB entries
"ga summary" | medium | Summarize GA allocations at job end
"ga stats" | high | Print GA usage statistics at job end
"ma summary" | medium | Summarize MA allocations at job end
"ma stats" | high | Print MA usage statistics at job end
"version" | debug | Print version number of all compiled routines
"tcgmsg" | never | Print TCGMSG debug information

# Top Level Print Control Specifications

The following example shows how a PRINT directive for the top level process can be used to limit printout to only essential information. The directive is

```
print none "ma stats" rtdb
```

This directive instructs the NWChem main program to print nothing, except for the memory usage statistics (ma stats) and the names of all items stored in the database at the end of the job.

The print level within a module is inherited from the calling layer. For instance, by specifying the print to be low within the MP2 module will cause the SCF, CPHF and gradient modules when invoked from the MP2 to default to low print. Explicit user input of print thresholds overrides the inherited value.
