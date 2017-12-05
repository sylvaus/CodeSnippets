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

    toString(): string {
        let text = "";
        let row : number;
        for (row = 0; row < this.rows; row++) {
            let col: number;
            for (col = 0; col < this.cols; col++) {
                text += this.array[row * this.cols + col] + " ";
            }
            text += "\n";
        }
        return text;
    }

    get(row: number, col: number): number {
        return this.array[row * this.cols + col]
    }

    set(row: number, col: number, value :number){
        this.array[row * this.cols + col] = value
    }
    
    scale(factor : number) {
    		return new Matrix(this.rows, this.cols, this.array.map((x) => {return x * factor;}));
    }

    mult(other: Matrix): Matrix {
        if (this.cols != other.rows) {
            return null;
        }

        let array = [];
        let row : number;
        for (row = 0; row < this.rows; row++){
            let col : number;
            for (col = 0; col < other.cols; col++){
                let scalar = 0;
                let index: number;
                for (index = 0; index < this.cols; index++) {
                    scalar += this.get(row, index) * other.get(index, col);
                }
                array.push(scalar);
            }
        }
        return new Matrix(this.rows, other.cols, array);
    }
    
    subMatrixWithoutRowCol(remove_row : number, remove_col : number) : Matrix {
    		let sub_array = [];
        let new_rows = this.rows;
        let new_cols = this.cols;
        let row : number;
        for (row = 0; row < this.rows; row++){
        		if (row == remove_row) {
            		new_rows -= 1;
            		continue;
            }
            let col : number;
            for (col = 0; col < this.cols; col++){
            		if (col == remove_col) {continue;}
                sub_array.push(this.array[row * this.cols + col]);
            }
        }
        if ((remove_col < this.cols) && (remove_col > -1)) {
        		new_cols -= 1;
        }
        return new Matrix(new_rows, new_cols, sub_array);
    }

    det(): number {
        if (this.cols != this.rows) {
            return 0;
        }
        
        if (this.cols == 1) {
            return this.array[0];
        }

        if (this.cols == 2) {
            return this.array[0] * this.array[3] - this.array[2] * this.array[1];
        }

        if (this.cols == 3) {
            return this.array[0] * (this.array[4] * this.array[8] - this.array[5] * this.array[7]) -
                this.array[1] * (this.array[3] * this.array[8] - this.array[5] * this.array[6]) +
                this.array[2] * (this.array[7] * this.array[3] - this.array[4] * this.array[6]);
        }
        
        let col : number;
        let result = 0;
        for(col = 0; col < this.cols; col++){
        		let sub_det = (this.subMatrixWithoutRowCol(0, col)).det()
            result += this.get(0, col) * sub_det;
        }
        return result;
    }
    
    cofactorMatrix() : Matrix {
    		let matrix = new Matrix(this.cols, this.rows, Object.assign([], this.array));
        let row : number;
        for (row = 0; row < this.rows; row++) {
            let col: number;
            for (col = 0; col < this.cols; col++) {
                matrix.set(row, col, ((-1) ** (col + row)) * (this.subMatrixWithoutRowCol(row, col)).det())
            }
        }
        
        return matrix;
    }

    transpose(): Matrix {
        let matrix = new Matrix(this.cols, this.rows, Object.assign([], this.array));
        let row : number;
        for (row = 0; row < this.rows; row++) {
            let col: number;
            for (col = 0; col < this.cols; col++) {
                matrix.set(col, row, this.get(row, col))
            }
        }
        return matrix;
    }

    inverse(): Matrix {
        if (this.cols != this.rows) {
            return null;
        }

        let det = this.det();
        if (Math.abs(det) > 0.0001) {
            if (this.cols == 2) {
                return new Matrix(2, 2, [this.array[3] / det, -this.array[1] / det,
                                         -this.array[2] / det, this.array[0] / det]);
            }
            else {
                return ((this.cofactorMatrix()).transpose()).scale(1.0 / det);
            }
        }
        else {
            return null;
        }

        
    }
}
```
