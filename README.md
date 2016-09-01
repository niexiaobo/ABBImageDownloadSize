# ABBImageDownloadSize
针对多线程下载图片后，分别获取对应图片Size，并更新对应UIImageView（1、父视图是UiView，直接更新Frame 2、父视图是UItableViewCell，单独更新对应一行Cell的Frame）



## 导入SDWebImage 

     pod 'SDWebImage'

## 在cellForRowAtIndexPath方法里：

//数据模型HZTheme
     HZTheme *theme = [self.dataArray objectAtIndex:indexPath.row];
     //除了其他数据额外添加两个image
@property (nonatomic,assign) double image_H;
@property (nonatomic,assign) double image_W;

     [tempImgView sd_setImageWithURL:[NSURL URLWithString:[NSString stringWithFormat:@"%@%@",AppInfoService,url]] placeholderImage:[UIImage imageNamed:@"acct_my_header_icon.jpg"] completed:^(UIImage *image, NSError *error, SDImageCacheType cacheType, NSURL *imageURL) {
                  DLog(@"=====%f====%f===",image.size.height,image.size.width);
                  
                  if (theme.image_H==0) {
                       theme.image_H=image.size.height;
                  theme.image_W=image.size.width;

                  [self.dataArray replaceObjectAtIndex:indexPath.row withObject:theme];
                  
                  //一个cell刷新
                  [tableView reloadRowsAtIndexPaths:[NSArray arrayWithObjects:indexPath,nil] withRowAnimation:UITableViewRowAnimationNone];
                  }
                 

              }];
