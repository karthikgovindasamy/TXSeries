This is to setup a ppc_connection port in TXSeries

we have created two programs fron.ccs and prog.ccs

Copy the fron.ccs to the region1 say ppc1 in the path /var/cics_regions/ppc1/bin/
Copy the prog.ccs to the region1 say ppc1 in the path /var/cics_regions/ppc1/bin/

Compile the two programs:
    cicstcl -elC fron.ccs
    cicstcl -elC prog.ccs

    fron.ccs will create two additional files fron and fron.o . Similarly, prog.ccs will create two addtional files prog and prog.o

    fron and prog are the executable files


Add Program Definition

    cicsadd -cpd -r ppc1 FRON PathName=fron
    cicsadd -cpd -r ppc2 PROG PathName=prog

Add Transaction Definition

    cicsadd -ctd -r ppc1 FRON ProgName=FRON
    cicsadd -ctd -r ppc2 PROG ProgName=PROG


Listener Definition is not required for ppc communication. It is done throught RL

You have to have communication Definition in both ppc_tcp

    cicsadd -ccd -r ppc1 CD01 RemoteLUName="ppc2"
    cicsadd -ccd -r ppc2 CD02 RemoteLUName="ppc1"