Routing and Navigation

This has examples of following topics as samples. you can use it for your project as a simple navigation example

1.) Basic routing.
2.) Wild card routing and route redirection
3.) Route parameters
4.) paramMap
5.) Optional Route
6.) Relative Route
7.) Child Routes

    1.) ng g c departments --it --is  (it - inline template),(is-inline style)
    2.) ng g c employees --it --is
    
    app-routing.module.ts
    { path: '', redirectTo: '/department-list', pathMatch: 'full' },  //default [route direction] on page load
    { path: 'department-list', component: DepartmentListComponent }, //changes from departments to department-list for relative routing..see code for more information
    { path: 'employees', component: DepartmentListComponent },
    { path: '**', component: NotFoundComponent } //[ wild card routes],
    //child routes example below
    {
    path: 'department-list/:id',
    component: DepartmentDetailComponent,
    children: [
      { path: 'overview', component: DepartmentOverviewComponent },
      { path: 'contact', component: DepartmentContactComponent }
    ]
  },
  //end child routes
  
  
  explanation of routes :
  
   private departmentId: number;
  constructor(private activatedRoute: ActivatedRoute, private router: Router) {

  }

  ngOnInit() {
    // this.departmentId = parseInt(this.activatedRoute.snapshot.paramMap.get("id"));
    this.activatedRoute.paramMap.subscribe((params: ParamMap) => {    //param map example as an observable to revert back on back button
      this.departmentId = parseInt(params.get("id"));
    });
  }
  goPrevious() {
    let previousId = this.departmentId - 1;
    // this.router.navigate(['/departments', previousId]);  absolute path routing
    this.router.navigate([{ id: previousId }], { relativeTo: this.activatedRoute }); //relative path routing
  }
  goNext() {
    let nextId = this.departmentId + 1;
    // this.router.navigate(['/departments', nextId]);
    this.router.navigate([{ id: nextId }], { relativeTo: this.activatedRoute }); ///append id to relative path routing
  }
  goBack() {
    let selectedId = this.departmentId ? this.departmentId : null;
    // this.router.navigate(["/departments", { id: selectedId }]);
    this.router.navigate(['../', { id: selectedId }], { relativeTo: this.activatedRoute });
  }
  showOverview() {
    this.router.navigate(['overview'], { relativeTo: this.activatedRoute });
  }
  showContact() {
    this.router.navigate(['contact'], { relativeTo: this.activatedRoute });
  }
  
  
  
  //Please download the code
  "npm install' to install depenedencies
  "ng serve" to see the examples working and to understand.
  
  Thank you
  
