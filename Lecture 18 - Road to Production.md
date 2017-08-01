# Road to Production

## 1 Code Review
## 2 Verification
> "Is the project being built correctly?"

Check the design rigorously against requirements.
Verify: Testing & Static Analysis (code check by software)

## 3 Validation
> "Will the project meet the user's needs?"

Check design against customers' needs
Verify: Beta Testing

## 4 Licensing
1. Proprietary (Copyrighted)
   * get rights as described
   * strict AF
   
2. General Public License (Copy-Left)
   * Mandatory no-profit software modules; never incorporated into proprietary software
   * open-access for software libraries, compiled binary code linked in proprietary programs
   
3. Berkely Software Distribution (BSD)
   * permissive open-source license; allows usage of code for anything
   
4. Mozilla Public License (MPL, Hybrid)
   * allows source code to be mixed (open-source + proprietary)
   * any file licensed under MPL must be open-source
   
5. Public Domain (License-Free)
   * no copyright owner
   * all enter this domain after 70 years

## 5 Maintenance
   * Rewrite:
      * Project scale: small
      * Tempting factors: high (badly structured code everywhere)
      * Pitfall: "Newer is better"
      * "Second System Effect"
      
   * Refactor:
      * Project scale: medium or larger
      * Tempting factor: low
      * preserving collective debugging/testing/refactoring knowledge
      
1. Corrective Maintenance
2. Adaptive Maintenance
3. Perfective Maintenance
4. Preventive Maintenance
