# BlandfordDelta

Notes and Scripts for using Kharma_Blandford on Delta

Quick Recap:

Two astrophysicists, Roger Blandford and Noemie Globus, describe in their paper found [here](https://arxiv.org/abs/2207.05839) and [here](https://academic.oup.com/mnras/article/514/4/5141/6609931) an alternate model of an accreting Black Hole. One of the central features of this model is the 'Ergomagnetosphere' a region close to the Black Hole ($\dot{M} \ll \dot{M}_{\text{Bondi}}$). This region is responsible for transporting energy outward from the Black Hole, but in turn requires that this region be devoid of any plasma.

Using [KHARMA](https://github.com/AFD-Illinois/kharma/tree/kharma-next) we can artifically create this model by injecting magnetic flux into the radial directions of the Black Hole within the region described by Blandford-Globus. The thought process is that if we can show that it is easy/hard (i.e. requires an unrealistically high magnetic flux) to create this ergomageosphere then it will give credence/critiscism to the model.
