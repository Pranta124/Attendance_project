# Attendance_project

# Index_Controller

```
public function index()
    {
        $employees=Employee::all();
        $attendance=Attendance::select('status')->distinct()->get();
        $attendances=Attendance::select('date_field')->distinct()->get();
        // dd($attendances);

//  dd($attendance);
        $employee=Employee::find(1);
        $a=Attendance::all();
        // dd($a);
        $query=DB::table('attendances')
        ->join('employees', 'employees.id', '=', 'attendances.employee_id')
        ->where('attendances.employee_id',1)
        // ->whereDate('attendances.created_at','2022-08-29')
        ->select('name','employee_id','status','attendances.created_at')
        ->selectRaw("SEC_TO_TIME(TIME_TO_SEC(TIMEDIFF(leave_time,entry_time) ) ) as 'total'")
        ->orderBy('employee_id', 'DESC')
        ->get();
        // dd($query);
        $update=DB::table('attendances')->where('attendances.date_field','2022-09-01')->get();
        //  dd($update);
        // dd($query);


//  dd($diffTimes);
     return view('attendance.index',compact('query','employee','employees','attendance','attendances','a'));
    }
```
