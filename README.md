A first attempt at implementing a linear natural deduction proof system for JILL has been accomplished. 

It includes a definition of a linear context, which then gets passed in the inference rules. The idea is to emulate linearity by only using lambda abstraction for the rules that use the intuitionistic context. 

This version still needs many changes before it can be considered a proper implementation.

The current version compiles, however it remains only a general idea of how one might emulate linearity. The hope is to get a working version by investigating JILL's sequent calculus which unlike natural deduction explicitly deals with the assumptions as well as the conclusion. 

For reference here are the rules of JILL's natural deduction (I will write G for the intuitionistic context, and D for the linear context):

Judgmental Rules:
													G ; D |- A true
   ------------hyp		-------------hyp!		   -----------------poss
	G ; A |- A 			  G,A ; . |- A 				G ; D |- A poss 


Multiplicative Connectives:

	G ; D |- A    G ; D' |- B 				G ; D |- A mAnd B      G ; D',A,B |- J
	-------------------------mAndI         -----------------------------------------mAndE
	   G ; D, D' |- A mAnd B 								G ; D, D' |- J

    												G ; D |- 1      G ; D' |- A
    	-----------1I							-----------------------------------1E
    	  G ; . |- 1 										G ; D, D' |- J

   		G ; D,A |- B 					G ; D |- A mImp B       G ; D' |- A
   	   -----------------mImpI 	       --------------------------------------mImpE
   	   	 G ; D |- A mImp B 						     G ; D, D' |- B


Additive Connectives:

	  G ; D |- A      G ; D |- B  			G ; D |- A aAnd B  			G ; D |- A aAnd B
	 -----------------------------aAndI    -------------------aAndEl   -------------------aAndEr
	         G ; D |- A aAnd B 					G ; D |- A   				G ; D |- B

	        										G ; D |- 0
	        ------------TI  					 ----------------0E
	         G ; D |- T 						   G ; D, D' |- J

	  		 G ; D |- A 					    G ; D |- B 				 
	  	  ------------------aOrIl  		    ---------------aOrIr
	  	    G ; D |- A aOr B 				  G ; D |- A aOr B

	  	        G ; D |- A aOr B      G ; D',A |- J      G ; D',B |- J
	  	       --------------------------------------------------------aOrE
	  	                      	       G ; D, D' |- J

Exponentials:

            G ; . |- A 				G ; D |- !A     G,A ; D' |- J
           -----------!I 		   ------------------------------!E
            G ; . |- !A 					G ; D, D' |- J

             G ; D |- A poss  				G ; D |- ?A     G ; A |- C poss
            -----------------?I  		   ---------------------------------?E
              G ; D |- ?A 								G ; D |- C poss