public class PathCreator
{
	public GameObject path;
	public Point head, tail, current;
	int size;
	public class Point
	{
		public Vector3 pos;
		public Point next;
	}
	void Start () 
	{
		size = 0;
		head = new Point();
		int i = 0;

    // Create our path based on the parent of the created waypoints assigned in inspector
    Transform[] children = path.GetComponentsInChildren<Transform>();
    
		foreach(Transform child in children)
		{
			if(i==0)
			{
				head.pos = child.position;
				tail = head;
				head.next = tail;
				i++;
			}
			else
			{
				Point curr = new Point();
				curr.pos = child.position;
				curr.next = head;
				tail.next = curr;
				tail = curr;
			}
			size++;
		}
		
		current = head;
	}
	
	public int getSize()
	{
		return size;	
	}
	
	public void CreateNewPath(GameObject newPath)
	{
		int i = 0;
		
		Transform[] children = newPath.GetComponentsInChildren<Transform>();
		foreach(Transform child in children)
		{
			if(i==0)
			{
				head.pos = child.position;
				tail = head;
				head.next = tail;
				i++;
			}
			else
			{
				Point curr = new Point();
				curr.pos = child.position;
				curr.next = head;
				tail.next = curr;
				tail = curr;
			}
		}
		
		current = head;
	}
	
	public Vector3 getClosestPoint(Vector3 pos)
	{
		Point curr = head;
		float min = 100000f;
		float dist;
		for(int i=0; i<size;i++)
		{
			dist = Vector3.Distance(curr.pos,pos);
			Debug.Log(dist);
			if(dist<min)
			{
				min = dist;
				current = curr;
			}
			curr = curr.next;
		}
		return current.pos;
	}
	
	public Vector3 startPath()
	{
		current = head;
		return current.pos;
	}
	
	public Vector3 getCurr()
	{
		current = current.next;
		return current.pos;
	}
}
