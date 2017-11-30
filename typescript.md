## matrix class
```
class Matrix {
    rows: number;
    cols: number;
    array: number[];

    constructor(rows: number, cols: number, array: number[]) {
        this.rows = rows;
        this.cols = cols;
        this.array = array;
    }

    get(row: number, col: number): number {
        return this.array[row * this.cols + col]
    }

    set(row: number, col: number, value :number){
        this.array[row * this.cols + col] = value
    }

    mult(other: Matrix): Matrix {
        if (this.cols != other.rows) {
            return null;
        }

        let array: number[];
        let row : number;
        for (row = 0; row < this.rows; row++){
            let col : number;
            for (col = 0; col < other.cols; col++){
                let scalar = 0;
                let index : number
                for (index = 0; index < this.cols; index++) {
                    scalar += this.get(row, index) * other.get(index, col);
                }
                array.push(scalar);
            }
        }
        return new Matrix(this.rows, other.cols, array);
    }
} 
```
