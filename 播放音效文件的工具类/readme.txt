
1、外层直接调用，传入URL就可以

2、可以选择震动播放和不震动播放

3、/** 清空音效文件的内存  
 
 *全局清空音效文件，应该在AppDelegate
 *- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application;
 *
 *局部清空音效文件,应该在当控制器收到内存警告时清空，
 *-(void)didReceiveMemoryWarning;
 *
 *遍历字典有个好处就是：stop，当条件达到了，找到了就stop了，就不需要再去遍历了
 */

比如：

-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
    
    //   00、创建url
    NSURL *url = [[NSBundle mainBundle] URLForResource:@"buyao.wav" withExtension:nil];
    //  01、不震动播放音效
    [PZLAudioTools playSystemSoundWithURL:url];
}

#pragma mark 清空全局的音效文件
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application
{
    [PZLAudioTools clearMemory];
    NSLog(@"%s",__func__);
}


#pragma mark 当前控制器收到内存警告时会调用的方法
- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // 局部音效需要在这里进行释放
    [PZLAudioTools clearMemory];
    NSLog(@"%s",__func__);
}