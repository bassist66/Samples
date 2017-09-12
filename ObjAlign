bool ObjAlign::SortTables(TArray<AActor*> &objs)
{
	float minDiffX = 100000.0f;
	float minDiffY = 100000.0f;
	float minX = objs[0]->GetActorLocation().X;
	float minY = objs[0]->GetActorLocation().Y;

	AActor* temp;

	// Sort based on Y value
	for (int i = 0; i < objs.Num(); i++)
	{
		for (int j = i + 1; j < objs.Num(); j++)
		{
			if (objs[j]->GetActorLocation().Y < objs[i]->GetActorLocation().Y)
			{
				temp = objs[i];
				objs[i] = objs[j];
				objs[j] = temp;
			}
		}
	}

	// Determine distance between the two endpoints of Y
	minDiffY = objs[0]->GetActorLocation().Y - objs[objs.Num() - 1]->GetActorLocation().Y;

	// Sort based on X Value
	for (int i = 0; i < objs.Num(); i++)
	{
		for (int j = i + 1; j < objs.Num(); j++)
		{
			if (objs[j]->GetActorLocation().X < objs[i]->GetActorLocation().X)
			{
				temp = objs[i];
				objs[i] = objs[j];
				objs[j] = temp;
			}
		}
	}

	// Determine distance between the two endpoints of X
	minDiffX = objs[0]->GetActorLocation().X - objs[objs.Num() - 1]->GetActorLocation().X;

	UE_LOG(LogTemp, Log, TEXT("%f"), minY);

	// Determine what direction to align based on which point distance is greater
	if (minDiffX > minDiffY)
	{
		//sort actors
		for (int i = 0; i < objs.Num(); i++)
		{
			for (int j = i + 1; j < objs.Num(); j++)
			{
				if (objs[j]->GetActorLocation().Y < objs[i]->GetActorLocation().Y)
				{
					temp = objs[i];
					objs[i] = objs[j];
					objs[j] = temp;
				}
			}
		}
		return true;
	}
	else
	{
		//sort actors
		for (int i = 0; i < objs.Num() - 1; i++)
		{
			for (int j = i + 1; j < objs.Num(); j++)
			{
				if (objs[j]->GetActorLocation().X < objs[i]->GetActorLocation().X)
				{
					temp = objs[i];
					objs[i] = objs[j];
					objs[j] = temp;
				}
			}
		}
		return false;
	}
}

bool ObjAlign::CheckAlignSpace(TArray<AActor*> &objs)
{
	TArray<AActor*> sortedObjs = objs;

	// if only 2 actors don't need to worry about space
	if (sortedObjs.Num() < 3)
		return true;

	if (SortTables(sortedObjs))
	{
		FVector startPos = sortedObjs[0]->GetActorLocation();
		FVector endPos = sortedObjs[sortedObjs.Num() - 1]->GetActorLocation();

		float dist = FMath::Abs(startPos.Y - endPos.Y);

		// Have enough space in Y to align, enable it
		if (dist >= sortedObjs.Num()*Cast<ATable>(sortedObjs[0])->radius)
			return true;
		else
			return false;
	}
	else
	{
		FVector startPos = sortedObjs[0]->GetActorLocation();
		FVector endPos = sortedObjs[sortedObjs.Num() - 1]->GetActorLocation();

		float dist = FMath::Abs(startPos.X - endPos.X);

		// Have enough space in X to align, enable it
		if (dist >= sortedObjs.Num()*Cast<ATable>(sortedObjs[0])->radius)
			return true;
		else
			return false;
	}
}
