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
# Update_function
```
  public function update_attendance(Request $request)
    {
        $id=$request->employee_id;
        $date=$request->date_field;
        // dd($id);

        $update = Attendance::where('employee_id',$id)
                            ->Where('date_field',$date)
                            ->first();
                        //  dd($update);
        $update =  Attendance::find($update->id);
        // dd($update);

        $update->employee_id = $request->input('employee_id');
        $update->date_field = $request->input('date_field');
        $update->status = $request->input('status');
        $update->reason = $request->input('reason');
        //   dd($update);
        $update->update();
        //   dd($update);
        return redirect('attendance')->with('status',"Job-Post Updated Successfully");

    }
```
