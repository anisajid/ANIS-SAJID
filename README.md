%let UID= 111222333;
%let libpath= C:\Users\msajid2\Desktop\SAS Ass3;
%let pdfpath= C:\Users\msajid2\Desktop\SAS Ass3;

libname HW3 "&libpath." ;
ods pdf file="&pdfpath.\HW3(How long to catch upto schedule)-&UID..pdf" ;

title "&SYSUSERID. - &UID. - How long to Catch up to Schedule - Final Exericse(2)" ;




/***************************** Macrotize Long Strings **********************************/

%let droprenamemv = (drop = CRSDepTime DepTime CRSArrTime ArrTime FirstDepTime WheelsOff WheelsOn Div1WheelsOn Div1WheelsOff Div2WheelsOn 
Div2WheelsOff Div3WheelsOn Div3WheelsOff Div4WheelsOn Div4WheelsOff Div5WheelsOn Div5WheelsOff 
rename =(CRSDepTimeF=CRSDepTime DepTimeF=DepTime CRSArrTimeF=CRSArrTime ArrTimeF=ArrTime FirstDepTimeF=FirstDepTime 
WheelsOffF=WheelsOff WheelsOnF=WheelsOn Div1WheelsOnF=Div1WheelsOn Div1WheelsOffF=Div1WheelsOff Div2WheelsOnF=Div2WheelsOn 
Div2WheelsOffF=Div2WheelsOff Div3WheelsOnF=Div3WheelsOn Div3WheelsOffF=Div3WheelsOff Div4WheelsOnF=Div4WheelsOn 
Div4WheelsOffF=Div4WheelsOff Div5WheelsOnF=Div5WheelsOn Div5WheelsOffF=Div5WheelsOff) ) ;

%let lengthmv = length Year 4. Quarter 4. Month 4. DayofMonth 4. DayOfWeek 4. FlightDate 8. UniqueCarrier $8. AirlineID  $4. 
Carrier  $4. TailNum  $10. FlightNum  4. OriginAirportID  $8. OriginAirportSeqID  $8. OriginCityMarketID  $6. Origin  $32. 
OriginCityName  $32. OriginState  $32. OriginStateFips  $32. OriginStateName  $32. OriginWac  $32. DestAirportID  $6. 
DestAirportSeqID  $6. DestCityMarketID  $6. Dest  $32. DestCityName  $32. DestState  $32. DestStateFips  $32. 
DestStateName  $32. DestWac  $32. CRSDepTime  $8. CRSDepTimeF 8. DepTime  $8. DepTimeF  8. DepDelay 4. DepDelayMinutes 4. 
DepDel15 4. DepartureDelayGroups 4. DepTimeBlk  $9. TaxiOut 4. WheelsOff  $8. WheelsOffF  8. WheelsOn  $8. WheelsOnF  8. 
TaxiIn 4. CRSArrTime  $8. CRSArrTimeF  8. ArrTime  $8. ArrTimeF  8. ArrDelay 4. ArrDelayMinutes 4. ArrDel15 4. 
ArrivalDelayGroups  4. ArrTimeBlk  $9. Cancelled 4. CancellationCode  $8. Diverted  4. CRSElapsedTime 4. ActualElapsedTime 4. 
AirTime 4. Flights 4. Distance 4. DistanceGroup 4. CarrierDelay 4. WeatherDelay 4. NASDelay 4. SecurityDelay 4. LateAircraftDelay 4. 
FirstDepTime  $8. FirstDepTimeF  8. TotalAddGTime 4. LongestAddGTime 4. DivAirportLandings 4. DivReachedDest 4. DivActualElapsedTime 4. DivArrDelay 4. 
DivDistance 4. Div1Airport  $8. Div1AirportID  $8. Div1AirportSeqID  $8. Div1WheelsOn  $8. Div1WheelsOnF  8. Div1TotalGTime 4. Div1LongestGTime 4. 
Div1WheelsOff  $8. Div1WheelsOffF  8. Div1TailNum  $8. Div2Airport  $8. Div2AirportID  $8. Div2AirportSeqID  $8. Div2WheelsOn  $8. Div2WheelsOnF  8. Div2TotalGTime 4. 
Div2LongestGTime 4. Div2WheelsOff  $8. Div2WheelsOffF  8. Div2TailNum  $8. Div3Airport  $8. Div3AirportID  $8. Div3AirportSeqID  $8. Div3WheelsOn  $8. Div3WheelsOnF  8. 
Div3TotalGTime 4. Div3LongestGTime 4. Div3WheelsOff  $8. Div3WheelsOffF  8. Div3TailNum  $8. Div4Airport  $8. Div4AirportID  $8. Div4AirportSeqID  $8. 
Div4WheelsOn  $8. Div4WheelsOnF  8. Div4TotalGTime 4. Div4LongestGTime 4. Div4WheelsOff  $8. Div4WheelsOffF  8. Div4TailNum  $8. Div5Airport  $8. Div5AirportID  $8. 
Div5AirportSeqID  $8. Div5WheelsOn  $8. Div5WheelsOnF  8. Div5TotalGTime 4. Div5LongestGTime 4. Div5WheelsOff  $8. Div5WheelsOffF  8. Div5TailNum   $8.  ; 

%let inputmv = input Year Quarter Month DayofMonth DayOfWeek FlightDate :yymmdd10. UniqueCarrier $ AirlineID $ Carrier $ TailNum $ FlightNum 
OriginAirportID $ OriginAirportSeqID $ OriginCityMarketID $ Origin $ OriginCityName $ OriginState $ OriginStateFips $ 
OriginStateName $ OriginWac $ DestAirportID $ DestAirportSeqID $ DestCityMarketID $ Dest $ DestCityName $ DestState $ 
DestStateFips $ DestStateName $ DestWac $ CRSDepTime $ DepTime $ DepDelay DepDelayMinutes DepDel15 DepartureDelayGroups 
DepTimeBlk $ TaxiOut WheelsOff $ WheelsOn $ TaxiIn CRSArrTime $ ArrTime $ ArrDelay ArrDelayMinutes ArrDel15 ArrivalDelayGroups 
ArrTimeBlk $ Cancelled CancellationCode $ Diverted CRSElapsedTime ActualElapsedTime AirTime Flights Distance DistanceGroup 
CarrierDelay WeatherDelay NASDelay SecurityDelay LateAircraftDelay FirstDepTime $ TotalAddGTime LongestAddGTime 
DivAirportLandings DivReachedDest DivActualElapsedTime DivArrDelay DivDistance Div1Airport $ Div1AirportID $ Div1AirportSeqID $ 
Div1WheelsOn $ Div1TotalGTime Div1LongestGTime Div1WheelsOff $ Div1TailNum $ Div2Airport $ Div2AirportID $ Div2AirportSeqID $ 
Div2WheelsOn $ Div2TotalGTime Div2LongestGTime Div2WheelsOff $ Div2TailNum $ Div3Airport $ Div3AirportID $ Div3AirportSeqID $ 
Div3WheelsOn $ Div3TotalGTime Div3LongestGTime Div3WheelsOff $ Div3TailNum $ Div4Airport $ Div4AirportID $ Div4AirportSeqID $ 
Div4WheelsOn $ Div4TotalGTime Div4LongestGTime Div4WheelsOff $ Div4TailNum $ Div5Airport $ Div5AirportID $ Div5AirportSeqID $ 
Div5WheelsOn $ Div5TotalGTime Div5LongestGTime Div5WheelsOff $ Div5TailNum  $ ;

%macro timevars ;
if CRSDepTime="2400" then do ;
	CRSDepTimeF=input("23:59", time5.) ; end ;
		else do ;
			format CRSDepTimeF time5. ;
			CRSDepTimeF=input(substr(CRSDepTime,1,2)||":"||substr(CRSDepTime,3,2), time5.) ; end ;
if DepTime="2400" then do ;
	DepTimeF=input("23:59", time5.) ; end ;
		else do ;
			format DepTimeF time5. ;
			DepTimeF=input(substr(DepTime,1,2)||":"||substr(DepTime,3,2), time5.) ; end ;
if CRSArrTime="2400" then do ;
	CRSArrTimeF=input("23:59", time5.) ; end ;
		else do ;
			format CRSArrTimeF time5. ;
			CRSArrTimeF=input(substr(CRSArrTime,1,2)||":"||substr(CRSArrTime,3,2), time5.) ; end ;
if ArrTime="2400" then do ;
	ArrTimeF=input("23:59", time5.) ; end ;
		else do ;
			format ArrTimeF time5. ;
			ArrTimeF=input(substr(ArrTime,1,2)||":"||substr(ArrTime,3,2), time5.) ; end ;
if FirstDepTime="2400" then do ;
	FirstDepTimeF=input("23:59", time5.) ; end ;
		else do ;
			format FirstDepTimeF time5. ;
			FirstDepTimeF=input(substr(FirstDepTime,1,2)||":"||substr(FirstDepTime,3,2), time5.) ; end ;
if WheelsOff="2400" then do ;
	WheelsOffF=input("23:59", time5.) ; end ;
		else do ;
			format WheelsOffF time5. ;
			WheelsOffF=input(substr(WheelsOff,1,2)||":"||substr(WheelsOff,3,2), time5.) ; end ;
if WheelsOn="2400" then do ;
	WheelsOnF=input("23:59", time5.) ; end ;
		else do ;
			format WheelsOnF time5. ;
			WheelsOnF=input(substr(WheelsOn,1,2)||":"||substr(WheelsOn,3,2), time5.) ; end ;
if Div1WheelsOn="2400" then do ;
	Div1WheelsOnF=input("23:59", time5.) ; end ;
		else do ;
			format Div1WheelsOnF time5. ;
			Div1WheelsOnF=input(substr(Div1WheelsOn,1,2)||":"||substr(Div1WheelsOn,3,2), time5.) ; end ;
if Div1WheelsOff="2400" then do ;
	Div1WheelsOffF=input("23:59", time5.) ; end ;
		else do ;
			format Div1WheelsOffF time5. ;
			Div1WheelsOffF=input(substr(Div1WheelsOff,1,2)||":"||substr(Div1WheelsOff,3,2), time5.) ; end ;
if Div2WheelsOn="2400" then do ;
	Div2WheelsOnF=input("23:59", time5.) ; end ;
		else do ;
			format Div2WheelsOnF time5. ;
			Div2WheelsOnF=input(substr(Div2WheelsOn,1,2)||":"||substr(Div2WheelsOn,3,2), time5.) ; end ;
if Div2WheelsOff="2400" then do ;
	Div2WheelsOffF=input("23:59", time5.) ; end ;
		else do ;
			format Div2WheelsOffF time5. ;
			Div2WheelsOffF=input(substr(Div2WheelsOff,1,2)||":"||substr(Div2WheelsOff,3,2), time5.) ; end ;
if Div3WheelsOn="2400" then do ;
	Div3WheelsOnF=input("23:59", time5.) ; end ;
		else do ;
			format Div3WheelsOnF time5. ;
			Div3WheelsOnF=input(substr(Div3WheelsOn,1,2)||":"||substr(Div3WheelsOn,3,2), time5.) ; end ;
if Div3WheelsOff="2400" then do ;
	Div3WheelsOffF=input("23:59", time5.) ; end ;
		else do ;
			format Div3WheelsOffF time5. ;
			Div3WheelsOffF=input(substr(Div3WheelsOff,1,2)||":"||substr(Div3WheelsOff,3,2), time5.) ; end ;
if Div4WheelsOn="2400" then do ;
	Div4WheelsOnF=input("23:59", time5.) ; end ;
		else do ;
			format Div4WheelsOnF time5. ;
			Div4WheelsOnF=input(substr(Div4WheelsOn,1,2)||":"||substr(Div4WheelsOn,3,2), time5.) ; end ;
if Div4WheelsOff="2400" then do ;
	Div4WheelsOffF=input("23:59", time5.) ; end ;
		else do ;
			format Div4WheelsOffF time5. ;
			Div4WheelsOffF=input(substr(Div4WheelsOff,1,2)||":"||substr(Div4WheelsOff,3,2), time5.) ; end ;
if Div5WheelsOn="2400" then do ;
	Div5WheelsOnF=input("23:59", time5.) ; end ;
		else do ;
			format Div5WheelsOnF time5. ;
			Div5WheelsOnF=input(substr(Div5WheelsOn,1,2)||":"||substr(Div5WheelsOn,3,2), time5.) ; end ;
if Div5WheelsOff="2400" then do ;
	Div5WheelsOffF=input("23:59", time5.) ; end ;
		else do ;
			format Div5WheelsOffF time5. ;
			Div5WheelsOffF=input(substr(Div5WheelsOff,1,2)||":"||substr(Div5WheelsOff,3,2), time5.) ; end ;
%mend ;

/**************** Reading the data in*******************/

data BTS201505 &droprenamemv. ;
infile "C:\Users\msajid2\Desktop\SAS Ass3\On_Time_On_Time_Performance_2015_5(1).csv"
dsd delimiter=',' firstobs=2 obs=max ;

	&lengthmv. ;

do while(not done);
	&inputmv. ;
	%timevars ;
		output ;
end;
run;

/*Sorting the data*/

proc sort data= BTS201505;
by Carrier TailNum FlightDate CRSDepTime FlightNum ;
run ;

/*Creating DepDelayInd for identifying position in a unique sequence for flights more than 15 minutes late*/

data EasterEgg1;
retain  DepDelayInd 0;  
format flightdate yymmdd10. DepDel15 4. DepDelay 4.;
set BTS201505;
by Carrier TailNum FlightDate ;

/*In case flight is not delayed DepDelayInd will be zero*/
if first.FlightDate=1 and DepDel15 ^= 1 then do;
DepDelayInd=0;
end;

/*Forming a sequence*/
else do ;
if first.FlightDate=1 and DepDel15 = 1 then do;
DepDelayInd=1;
end;
else do ;
if DepDel15 =1 then do;
DepDelayInd+1;
end;
else do; 
DepDelayInd = 0;  
end;
end;
end;
output ;

run ;

/*Getting rid where DepDelayInd=0 or retaining only flights which are part of a sequence*/
data EasterEgg2;
format flightdate yymmdd10. ;
set EasterEgg1(keep= Carrier TailNum FlightDate DepDelayInd DepDelay Origin Distance CarrierDelay WeatherDelay NASDelay SecurityDelay LateAircraftDelay );
by Carrier TailNum FlightDate ;
if DepDelayInd ^=0 then do ;
output ;
end;
run;

/*Assigning sequence ID to every sequence & incrementing*/
data EasterEgg3_withSeqID;
retain SeqID 0;
format flightdate yymmdd10. ;
set EasterEgg2;
by Carrier TailNum FlightDate ;
if DepDelayInd =1 then do ;
SeqID+1;
end;
output ;
run;

/*Creating Summary*/
data Summary ; 
retain EndSeq 1 FirstDelayCause FirstOrigin SequenceDist;
format flightdate yymmdd10. ;
set EasterEgg3_withSeqID;
by Carrier TailNum FlightDate SeqID ;
if first.SeqID then do ;

/*Identifying the cause of the delay for first flight*/
	if CarrierDelay >= WeatherDelay and 
		CarrierDelay>= NASDelay and CarrierDelay>= SecurityDelay and CarrierDelay>= LateAircraftDelay then do;
	FirstDelayCause='CarrierDelay';
	end;
	if WeatherDelay >= CarrierDelay and 
		WeatherDelay>= NASDelay and WeatherDelay>= SecurityDelay and WeatherDelay>= LateAircraftDelay then do;
	    FirstDelayCause='WeatherDelay';
	end;
	if NASDelay >= CarrierDelay and 
			NASDelay>= WeatherDelay and NASDelay>= SecurityDelay and NASDelay>= LateAircraftDelay then do;
	FirstDelayCause='NASDelay';
	end;
	if SecurityDelay >= CarrierDelay and 
			SecurityDelay>= WeatherDelay and SecurityDelayy>= NASDelay and SecurityDelay>= LateAircraftDelay then do;
	FirstDelayCause='SecurityDelay';
	end;
	if LateAircraftDelay >= CarrierDelay and 
			LateAircraftDelay>= WeatherDelay and LateAircraftDelay>= NASDelay and LateAircraftDelay>= SecurityDelay then do;
	FirstDelayCause='LateAircraftDelay';
	end;

/*Identifying origin of first flight*/
FirstOrigin = Origin;
SequenceDist = Distance ;
end;

/*Total numbers of miles flown in the sequence*/
else do;
SequenceDist+Distance;
end;

/*EndSeq for sequence number in the delay sequence which identifies the position in a particular sequence where tailnumber is returned to normal*/
if last.SeqID then do;
EndSeq=DepDelayind+1;
end;

run;

/*sorting the flight by carrier tailnum date & SeqID*/
data SummaryFinal ; 
format flightdate yymmdd10. ;
set Summary;
by Carrier TailNum FlightDate SeqID ;
if  last.SeqID then do;
output ;
end;
run;

/********************************************************************************/
/********************* Summary Statistics ***************************************/
/********************************************************************************/
proc freq data=Summary;
tables EndSeq / plot=freqplot;
run;

proc univariate data=Summary;
var EndSeq;
histogram EndSeq / normal lognormal (theta=-25) kernel (k = triangular /* c = SJPI /* Default is MISE*/ /*w = 1*/ color = green ) ;
run ;

proc means data=Summary min max mean std skew kurt ;
var EndSeq;
run;

proc means data=Summary min max mean std skew kurt ;
var EndSeq;
by carrier;
run;

/********************************************************************************/
/********************* Poisson Model ***************************************/
/********************************************************************************/

proc genmod data = Summary; 
class FirstOrigin FirstDelayCause /param=glm; 
model EndSeq= SequenceDist FirstDelayCause FirstOrigin / dist=poisson link=log offset = EndSeq; 
output out=poisson1 pred=pred ; 
run ; 

/*********************Explanation***************************************/

/*Inspecting the Summary Statistics EndSeq gives the following insights:
-	Most Flight delay sequence ended after first flight (as it has the maximum frequency as depicted by frequency distribution and it is also mode)and EndSeq id of 2
-	Since the mean of EndSeq variable is 2.82 it means on average it takes 2 flights for a tail number to return to on-time status (i.e. EndSeq ID 3 returned the tail number to normal time)
-	Among Airlines AA has the lowest mean of EndSeq variable (i.e. 2.49) while NK has the highest mean (i.e. 3.41) which means on average a tail number in AA takes the least number of flights to return to on-time status as compared to NK which takes the maximum number of flights on average for a tainumber to return to normal

Inspecting the co-efficents of the Poisson regression model depicts the following information:
- With every one unit increase in SequenceDist reduces the log EndSeq by -0.0003. In other words if sequence distance increased it takes less number of flights to get the schedule back to normal
- Whenever First Delay cause is Carrier Delay it takes less number of flights to get the schedule back to normal as compared to Weather Delay. However, whenever First Delay Cause is Late Aircraft and NAS Delay it takes more number of flights to get the schedule back to normal as compared to Weather Delay
- All the first delay causes and SeqDistance variables had a statistically significant relationship with ln SequenceDist
- YUM was the reference for the first origin variable
- Out of 290 first origin variable 201 were found to have a statistically significant relationship (with p-value less than 0.05)
- For 147 first origins (due to positive co-efficient) as compared to YUM it takes more number of flights to get the schedule back to normal.
- For 54 first origins (due to negative co-efficient) as compared to YUM it takes less number of flights to get the schedule back to normal.

*/

ods pdf close ;
ANIS-SAJID
