```
if(temp.layer==17 || temp.layer==9)
{
    // grab a ref to the projectile's
    aProj=tempGO.GetComponent<ProjectileControl
    ler>();
    
    // quick check to make sure that this
    // projectile was not launched by this player
    if (aProj.ownerTypeId != id ) 
    {
        // tell the hit function about this
        // collision, passing in the
        // gameobject so that we can
        // get to its projectile controller
        // script and find out more about
        // where it came from
        Hit();
        // tell our battle controller that we
        // got hit
        battleControl.Fragged();
    }
    
    // tell the global battle controller
    // who fragged us
    GlobalBattleManager.Instance.RegisterFrag(
        ( aProj.ownerTypeId id);
    );
}

public void OnTriggerEnter( Collider other )
{
    // check to see if the trigger uses any of the layers where
    // we want to automatically respawn the player on impact
    int objLayerMask = (i << other.gameObject.layer);
    
    if ((respawnLayerMask.value & objLayerMask) > 0)
    {
        Respawn();
    }
}

void Hit()
{
    // reduces lives by one
    myDataManager.ReduceHealth(1);
    
    if (myDataManager.GetHealth()<1) // destroyed
    {
        isRespawning=true;
        
        // blow up! (apply a force to affect everything in
        // the vicinity and let's get the model spinning
        // too, with angular velocity)
        myBody.AddExplosionForce(myBody.mass * 2000f,
        myBody.position, 100);
    }

```