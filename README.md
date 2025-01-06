Use A or D to change lanes  
Download and extract zip file	  
run exe file	  
.exe file only works on windows	  
Please refer to raw text file as this view is bugged  
It contains missing text  





                        
1.Code to move player-
            
[SerializeField] GameObject GmCanvas;  
Rigidbody body;  
bool canright;  
bool canleft;  
int lane;  
Vector3 Lpos=new Vector3 (-2.5f,1f,0);  
Vector3 Rpos = new Vector3(2.5f, 1f, 0);  
Vector3 Mpos = new Vector3(0, 1f, 0);  
// Start is called before the first frame update  
void Start()  
{  
    body = GetComponent<rigidbody>();  
    lane = 1;  
    movelane();  
}  
  
// Update is called once per frame
void Update()
{
    if (Input.GetKeyDown(KeyCode.D) & canright == true)
    {
        lane++;
        movelane();

    }
    if (Input.GetKeyDown(KeyCode.A) & canleft == true) { 
        lane--;
        movelane();
    }

}
private void FixedUpdate()
{
    
}
void movelane() {
    if (lane==1) { 
        transform.position = Mpos;
        canright = true;
        canleft = true;
    }
    if (lane == 2) { 
        transform.position = Rpos;
        canright = false;
        canleft = true;
    }
    if (lane == 0) { 
        transform.position = Lpos;
        canleft = false;
        canright= true;
    }
}
private void OnTriggerEnter(Collider other)
{
    if (other.tag=="Player")
    {
        Time.timeScale = 0;
        GmCanvas.SetActive(true);
    }
}

2.Code to spawn obstacles-

[SerializeField]GameObject obs;
float timer;
float count = 1.4f;
int rand;
Vector3 obspos;
void Start()
{
    spawnobs();
    timer=count;
}

// Update is called once per frame
void Update()
{
    timer = timer - Time.deltaTime;
    if (timer < 0) {
        spawnobs();
        timer = count;
        rand=Random.Range(0, 3);
    }
}
void spawnobs() {
    if (rand == 0) { obspos = new Vector3(2.5f, transform.position.y, transform.position.z); }
    if (rand == 1) { obspos = new Vector3(-2.5f, transform.position.y, transform.position.z); }
    if(rand == 2) { obspos = new Vector3(0, transform.position.y, transform.position.z); }
    obs=Instantiate(obs,obspos,Quaternion.Euler(-90f,0,0));
    Destroy(obs,5);
}
