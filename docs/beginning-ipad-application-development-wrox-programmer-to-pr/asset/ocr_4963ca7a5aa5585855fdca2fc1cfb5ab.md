```
@synthesize browser;
@synthesize services;

//---set the number of rows in the TableView---
- (NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section {
    return [services count];
}

//---display the individual rows in the TableView---
- (UITableViewCell *)tableView:(UITableView *)tableView
cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    static NSString *CellIdentifier = @"Cell";

    UITableViewCell *cell = [tableView
        dequeueReusableCellWithIdentifier:CellIdentifier];
    if (cell == nil) {
        cell = [[[UITableViewCell alloc]
            initWithStyle:UITableViewCellStyleDefault
            reuseIdentifier:CellIdentifier] autorelease];
    }

    //---display the hostname of each service---
    cell.textLabel.text = [[services objectAtIndex:indexPath.row] hostName];

    return cell;
}

//---browse for services---
- (void) browseServices {
    services = [NSMutableArray new];
    self.browser = [[NSNetServiceBrowser new] autorelease];
    self.browser.delegate = self;
    [self.browser searchForServicesOfType:@"_MyService._tcp." inDomain:@""];
}

- (void)viewDidLoad {
    debug.text = @"";
    [self browseServices];
    [super viewDidLoad];
}

//---services found---
- (void)netServiceBrowser:(NSNetServiceBrowser *)aBrowser
    didFindService:(NSNetService *)aService
    moreComing:(BOOL)more {

    [services addObject:aService];
    debug.text = [debug.text stringByAppendingString:
        @"Found service. Resolving address...\n"];
    [self resolveIPAddress:aService];
}
```