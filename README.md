Implementation of the logical frameworks linctx, added, merge and asmp. These were then used to define JILL's natural deduction and sequent calculus. 

To keep the linear context unordered the cons operation of linctx inserts the new formula between two contexts. This is turn affects the implementation of added and merge. 

Asmp is needed for hyp!, and each rule that deals with the intuitionistic assumptions. 

For reference here are the rules of JILL's sequent calculus: 


Judgmental Rules:

	G, A; D, A => Ga									G ; D => A ; .			
	-----------------copy		   -------------init	-------------promote		   
	G, A; D => Ga				 	 G ; A => A ; .	    G ; D => . ; A


Multiplicative Connectives:

	G ; D => A ; .    G ; D' => B ; .			               G ; D,A,B => Ga
	-------------------------------mAndR                     ----------------------mAndL
	   G ; D, D' => A mAnd B ; .								G ; D, A mAnd B => Ga

    															 G ; D => Ga
    	---------------1R					                ----------------------1L
    	  G ; . => 1 ; . 										G ; D, 1 => Ga

   		G ; D,A => B ; .					G ; D => A ; .       G ; D',B => Ga
   	   ---------------------mImpR 	       --------------------------------------mImpL
   	   	 G ; D => A mImp B ; .					     G ; D, D', A mImp B |- Ga


Additive Connectives:

G ; D => A ; .      G ; D => B ; .  			G ; D, A => Ga  			     G ; D, B => Ga 
-----------------------------aAndR    		 -------------------aAndEl         ------------------aAndEr
	    G ; D => A aAnd B ; .					G ; D, A aAnd B  => Ga   	    G ; D, A aAnd B  => Ga

	        										
	        --------------TR  					 ----------------0L
	         G ; D => T ; . 					  G ; D, 0 => Ga

	  		 G ; D => A ; .					    G ; D => B ; . 				 
	  	  ------------------aOrRl  		      -----------------aOrRr
	  	    G ; D => A aOr B ; . 			   G ; D => A aOr B ; .

	  	        G ; D, A => Ga     G ; D, B => Ga     
	  	       ---------------------------------------aOrL
	  	                      G ; D, A aOr B => Ga

Exponentials:

            G ; . => A ; . 				     G,A ; D => Ga
           ---------------!R 		       ------------------!L
            G ; . => !A ; .					G ; D, !A => Ga

             G ; D => . ; A  				G ; A => . ; C 
            -----------------?R  		   ------------------?L
              G ; D => ?A ; . 				G ; ?A => . ; C 